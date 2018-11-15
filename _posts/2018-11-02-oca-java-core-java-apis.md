---
layout: post
title:  "OCA: Core Java APIs"
date:   2018-11-02 11:33:27 +0100
categories: OCA Java 1.8
---
A year ago I succesfully obtained the Java 1.8 OCA certificate. I made some summaries to help me study for the accompanying exam. In this blog I'll share the summaries. This one is about Core Java APIs.

# Creating and manipulating Strings

- String:
  - Sequence of characters
  - Reference type
  - &quot;new&quot; keyword not mandatory for instantiation

## Concatenation

- + operator:
  - combines two String objects = concatenation
  - can be used in two ways within same line
  - rules:
    - if both operands are numeric: + means numeric addition
    - if either operand is String: + means concatenation
    - evaluated left to right

