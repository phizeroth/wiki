---
title: C++ Data Types
description: 
published: true
date: 2022-04-11T16:58:35.925Z
tags: arduino, code
editor: markdown
dateCreated: 2022-04-11T16:58:35.925Z
---

## Integer Data Types

C type             | Arduino    | stdint.h   | bytes | range
:------------------|:-----------|:-----------|:------|:-----
`boolean` or `bool`|            |            | `1`   | `0, 1`
`unsigned char`    | `byte`     | `uint8_t`  | `1`   | `0 .. 255`
`char`             |            | `int8_t`   | `1`   | `-128 .. 127`
`unsigned short`   | `word`     | `uint16_t` | `2`   | `0 .. 65,535`
`short`            |            | `int16_t`  | `2`   | `-32,768 .. 32,767`
`unsigned int`     |            | `uint32_t` | `4`   | `0 .. 4,294,967,295`
`int`              |            | `int32_t`  | `4`   | `-2,147,483,648 .. 2,147,483,647`
`unsigned long`    |            | `uint64_t` | `8`   | `0 .. 18,446,744,073,709,551,615`
`long`             |            | `int64_t`  | `8`   | `-9,223,372,036,854,775,808 .. 9,223,372,036,854,775,807`

## Floating Point Data Types

type | IEE754 name | bytes | range
|:-|:-|:-|:-|
`float`  | single precision | 4 | `-3.4e38 .. 3.4e38`
`double` | double precision | 8 | `-1.7e308 .. 1.7e308`