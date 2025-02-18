---
title: scripting
description: 
published: true
date: 2025-02-18T10:12:47.381Z
tags: 
editor: markdown
dateCreated: 2025-02-15T20:11:31.137Z
---

# Linux BASH Scripting

## General

```bash
'#!/bin/bash' - shebang; indicates the start of a script file
echo - outputs text to the terminal
755 - permisions for the script files
a= - this is how to define variables
$a - this is how to output variables
read [variable] - reads user input and stores it in the variable
```

## If Statement

```bash
if [condition]; then
	echo [text]
else
	echo [text]
fi
```

## For Statement

```bash
for i in [range]; do
	echo [text]
done
```

## While Loop

```bash
count=1
while [count -le 3]; do
	echo ["Number: " $i]
done
```

## Case Statement

```bash
case <variable> in
    <pattern1>)
        # commands for pattern1
        ;;
    <pattern2>)
        # commands for pattern2
        ;;
    ...
    *)
        # default commands
        ;;
esac
```

## Functions

```bash
greet(){
	echo "Hello, $1!"
}
greet "Bob"

In this case $1 represents the first parameter passed to the function
```

## Operators

### String Comparison Operators

```bash
= - checks if two strings are equal
!= - checks if two strings are not equal
< - checks if one string is less than another (lexicographically)
> - checks if one string is greater than another (lexicographically)
-n - checks if the string length is non-zero
-z - checks if the string length is zero
```

### Numeric Comparison Operators

```bash
-eq - checks if two numbers are equal
-ne - checks if two numbers are not equal
-lt - checks if one number is less than another
-le - checks if one number is less than or equal than another
-gt - checks if one number is greater than another
-ge - checks if one number is greater than or equal than another
```

### File Comparison Operators===

```bash
-e - checks if the file exists
-f - checks if the file exists and is a regular file
-d - checks if the directory exists
-r - checks if the file is readable
-w - checks if the file is writable
-x - checks if the file is executable
-s - checks if the file is not empty
-nt - checks if one file is newer than the other
-ot - checks if one file is older than the other
```

### Logical Operators

```bash
&& - logical AND
|| - logical OR
! - logical NOT
```

You can combine multiple conditions using -a (AND) and -o (OR) within the same [ ... ] or [[ ... ]] blocks.
Use double square brackets [[ ... ]] for conditional expressions: It provides more features and fewer pitfalls compared to single square brackets [ ... ].
Quote variables: Always quote your variables to prevent word splitting and globbing issues.
Use spaces: Ensure spaces around the brackets and operators for correct parsing.