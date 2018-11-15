Deze stappen moet je volgen om typescript coverage in Sonar te verkrijgen.

1. Properties pom.xml van front-end
Voeg onderstaande properties toe aan pom.xml van de front-end. Op deze manier weer Sonar waar er gezocht moet worden naar de test-coverage.
~~~~
  <sonar.typescript.lcov.reportPaths>${project.basedir}/coverage/lcov.info</sonar.typescript.lcov.reportPaths>
  <sonar.sources>${project.basedir}/src/</sonar.sources>
  <sonar.language>ts</sonar.language>
~~~~
2. frontend-maven-plugin
Er moet aan de frontend-maven-plugin duidelijk gemaakt worden dat die coverage reports aangemaakt moeten worden. Hiervoor kan je een execution toevoegen die 'npm run testCoverage' uitvoert:
~~~~
   <execution>
     <id>npm test coverage</id>
     <goals>
       <goal>npm</goal>
     </goals>
     <configuration>
       <arguments>run testCoverage</arguments>
       <skip>${coverage.skip}</skip>
     </configuration>
   </execution>
~~~~
3. npm script in package.json
Dat npm-script dient toegevoegd te worden en komt overeen met het volgende npm script in je package.json:
~~~~
   "scripts": {
       "testCoverage": "ng test opdrachten-production --watch=false --browsers ChromeHeadless --code-coverage",
   }
~~~~
Indien in angular.json sourceMap op false staat dien je aan het npm script ook "–sourceMap" toe te voegen:
~~~~
   "scripts": {
       "testCoverage": "ng test opdrachten-production --watch=false --sourceMap --browsers ChromeHeadless --code-coverage",
   }
~~~~
Jenkins toont misschien foutmeldingen in verband met niet gevonden regelnummers. In dat geval is "–sourceMap" niet toegevoegd.

Voorbeeld foutmelding: 

[WARNING] Problem during processing LCOV report: can't save DA data for line 47 of coverage report file (java.lang.IllegalArgumentException: Line with number 19 doesn't belong to file src/app/app.component.ts).
4. Aanpassingen in karma.conf.js
Er moet een aanpassing gebeuren in karma.conf.js van de angular app.
~~~~
plugins: [
      ...
      require('karma-jasmine-html-reporter'),
      require('karma-coverage-istanbul-reporter')
      ....
  ],
  coverageIstanbulReporter: {
      reports: ['html', 'lcovonly'],
      fixWebpackSourcePaths: true
  },
  reporters: config.angularCli && config.angularCli.codeCoverage
            ? ['progress', 'coverage-istanbul']
            : ['progress', 'kjhtml'],
~~~~
5. DevDependencies package.json
Je moet de volgende dependencies in de devDependencies van package.json toevoegen indien ze nog niet aanwezig zijn:
~~~~
  "devDependencies": {
      ...
      "karma-coverage-istanbul-reporter": "1.2.1",
      "karma-jasmine-html-reporter": "0.2.2",
      ...
  }
~~~~
6. NodeJs op Jenkins
Indien Jenkins de boodschap toont dat NodeJs niet gevonden is kan je 1 van deze 2 dingen doen:

- Je kan in de Jenkins configuratie expliciet "Provide node and npm" aanvinken.
- Je kan aan pom.xml volgende property toevoegen: '<sonar.typescript.node>${project.basedir}/node/node</sonar.typescript.node>'
De SonarTS plugin weet hierdoor dat de node executable van daar moet gebruikt worden. (Deze werd eerder geinstalleerd door de frontend-maven-plugin). 
7. Lokaal testen
Lokaal testen kan met 'npm run testCoverage'. Dit generaart een folder 'coverage' met file lcov.info.
