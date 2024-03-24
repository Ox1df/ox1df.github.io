---
layout: post
title: Regex Expressions in Linux
date: 2024-02-18
categories: [Linux, Command Line, Regular Expressions]
tags: [Regex, Bash, Text Processing]
author: YourName
image:
  path: 
  alt: Regular Expressions in Linux
---

Hey! Pentesters Myself 0x1df
This article will explain regular expressions in Linux in an easy-to-understand way. We'll cover the basics, like what special characters mean, and show you practical examples of how to use them. We'll also talk about different versions of regular expressions and how they work on different Linux systems.
Regular expressions (regex) are powerful tools for pattern matching and text manipulation in Linux. They allow you to search for patterns within files, filter text output, and perform various text processing tasks efficiently. This guide will cover the basics of using regex in Linux command-line environments.


# Introduction to Regular Expressions


Regular expressions, often called RegEx, are handy tools for finding and manipulating text in Linux and other programming languages. They let you create patterns to search for specific words or patterns within a bunch of text. You've probably seen them in commands like `grep` or `sed` when you're searching for files or changing text. Regular expressions, or regex, are special sequences of characters that help you find and manipulate text. They act like powerful search patterns, allowing you to locate specific words, phrases, or patterns within a larger body of text.

In Linux, regular expressions are commonly used in commands to search for files, modify text, and filter data. They're like secret codes that help you quickly find what you're looking for.

In this guide, we'll learn the basics of regular expressions, including how to use them in Linux commands. By the end, you'll be able to use regex to search for text patterns and perform tasks more efficiently on your Linux system.



## Basic Regex Syntax
Regular expressions (regex) are sequences of characters that define a search pattern. They're incredibly useful for finding specific patterns within text. Let's delve into some basic syntax elements:

### Literal Characters

Literal characters in regex are characters that match themselves exactly. When you include a literal character in a regex pattern, the pattern will only match that specific character in the text.

For example:
```zsh
    The regex pattern hello will match the word "hello" wherever it appears in the text.
    The regex pattern abc will match the sequence "abc" wherever it appears in the text.
```
Literal characters are the simplest elements of a regex pattern and are used to find exact matches of specific strings in the text.
### Character Classes
Character classes in regex allow you to define a set of characters that can match at a particular position in the text. They are denoted by square brackets [ ] and can match any single character from the set.

For example:
```zsh
    The character class `[aeiou]` matches any vowel `(i.e., 'a', 'e', 'i', 'o', 'u')`.
    The character class `[0-9]` matches any digit from 0 to 9.
    The character class `[a-zA-Z]` matches any lowercase or uppercase letter.
```
You can also use character ranges within character classes to specify a range of characters. For example, `[a-z]` matches any lowercase letter from `a` to `z`, and `[A-Z]` matches any uppercase letter from `A` to `Z`.

Character classes are useful when you want to match any character from a specific set or range of characters in the text. They provide a flexible way to define patterns that can match a variety of characters at a particular position.
### Anchors
Anchors in regex are special characters that allow you to match positions rather than actual characters in the text. They are used to specify where in the text a match should occur. The two most common anchors are:

    `^ (caret)`: This anchor matches the beginning of a line or string.

    For example:
        The regex `^hello` matches the word "hello" only if it appears at the beginning of a line or string.
        In the text "hello world", the regex `^hello` will not match anything because "hello" does not appear at the beginning of the line.

    `$ (dollar sign)`: This anchor matches the end of a line or string.

    For example:
        The regex world$ matches the word "world" only if it appears at the end of a line or string.
        In the text "hello world", the regex world$ will match "world" because it appears at the end of the line.

Anchors are useful for specifying the exact position where a match should occur within the text. They help you make your regex patterns more precise and specific.
### Quantifiers
Quantifiers in Linux regular expressions are symbols or characters used to specify the quantity of the preceding element in a pattern. They allow you to define how many times a particular character, group, or character class should be matched in a string. Here are some common quantifiers:

- `*`: Matches zero or more occurrences of the preceding element.
- `+`: Matches one or more occurrences of the preceding element.
- `?`: Matches zero or one occurrence of the preceding element.
- `{n}`: Matches exactly n occurrences of the preceding element.
- `{n,}`: Matches n or more occurrences of the preceding element.
- `{n,m}`: Matches between n and m occurrences of the preceding element, inclusive.


## Using Regex in Linux Commands
Regular expressions (regex) are powerful tools for pattern matching and text manipulation in Linux commands. They allow you to search for, match, and manipulate text based on specified patterns. Here's how you can use regex in some common Linux commands:

### grep
`grep` is a command-line utility for searching text patterns in files or streams. It supports regex, allowing you to perform complex pattern matching operations.For example, you can use grep to search for lines in a file that contain a specific word or match a particular pattern.
#### Basic Usage

To search for a specific pattern in a file, you can use `grep` followed by the regex pattern and the file name:

```bash
grep "pattern" filename
```
##### Options

   ` -E `or `--extended`-regexp: Enables extended regex syntax, allowing for more complex pattern matching.
    `-i `or `--ignore-case`: Ignores case distinctions in both the pattern and the input files.
    `-v` or `--invert-match`: Inverts the match, displaying lines that do not match the pattern.
    `-r `or `--recursive`: Recursively searches through directories.

**Common Regex Patterns**



- `.`: Matches any single character.
- `^`: Matches the start of a line.
- `$`: Matches the end of a line.
- `[]`: Matches any single character within the brackets.
- `[^]`: Matches any single character not within the brackets.
- `*`: Matches zero or more occurrences of the preceding element.
- `+`: Matches one or more occurrences of the preceding element.
- `?`: Matches zero or one occurrence of the preceding element.
- `|`: Acts as an OR operator, allowing multiple patterns to be matched.
- `\`: Escapes special characters.


**Search for lines starting with "hello":**

```bash

grep "^hello" filename
```

**Search for lines containing "apple" or "orange":**
```bash

grep "apple\|orange" filename
```

**Search for lines ending with "world" ignoring case:**

```bash

grep -i "world$" filename
```

**Search recursively for "error" in all files within a directory:**

```bash

grep -r "error" director
```
### sed
Using `sed` in regex allows you to perform text transformations and manipulations based on regular expressions. Here's a brief overview:
`sed (Stream Editor)` and Regex
sed is a powerful command-line utility for processing text streams. When combined with regular expressions,it becomes a versatile tool for pattern-based text editing.

**Basic Usage**
```bash
sed 's/pattern/replacement/' filename

```
    `s`: Indicates substitution.
    `pattern`: Regular expression pattern to match.
    `replacement`: Text to replace the matched pattern.
    `filename`: Name of the file to operate on.


**Sed address format**

Assume we have a list given below 
```shell
#cat iamlist.txt

1. Linux 
2. senpai
3. syntax
4. pukka
5. Storage
6. paylist

```
so indeed we want print out the desire word or replace so we can use below syntax

```shell
sed -n '2'p iamlist.txt
2. senpai
#for replacing the text
sed -i '2s/.*/baka/' iamlist.txt


```
so what happened here

- `-i`: This option edits files in place.
- `2:` Specifies the line number.
- `s`: Indicates a substitution command in sed.
- `.*`: Represents the entire line.
- `baka`: The text you want to replace the line with.
- `iamlist.txt`: The name of the file.




**Print Lines: Print each line of a file:**

```bash

sed 'p' filename
```

**Search and Replace: Substitute one string with another:**

~~~bash

sed 's/old_string/new_string/g' filename
~~~

**Delete Lines: Remove specific lines based on a pattern:**

```bash

sed '/pattern/d' filename
```

**Insert Text: Insert text before or after specific lines:**

```bash

    sed '3i\New line' filename  # Insert before line 3
    sed '3a\New line' filename  # Insert after line 3
```
Flags:

- `-n`: Suppress automatic printing of pattern space.
- `-i`: Edit files in-place (overwrite original file).
- `-e`: Specify multiple commands or scripts.
### awk
`awk` is a powerful text-processing tool available in Unix and Unix-like operating systems, including Linux. 
It is primarily used for pattern scanning and processing of text files.what if i master it huhu!!! as to me awk has bit complex to me so for now i gone to surface level only if you can master it you will be a batman in linux

**Basic Syntax:**
```bash
awk 'pattern { action }' filename
```
- Pattern:

    Defines the condition or pattern to match.
    If omitted, the action will be performed on every line.
    Patterns can be regular expressions.

- Action:

    Defines the action to be taken when the pattern matches.
    If omitted, awk will perform the default action, which is to print the entire line.

assume we have a list champ.txt
```bash
cat champ.txt

pulka dev account 45000
hinata pentester account 25000
shruthi soc account 100000
varun SDE account  50000
pulka dev account 45000
binod  pentester account 25000
Alle Alle  account 100000
kandu SDE account  50000
```
by default we use below syntax
- to print whole list 
```shell
awk '{print}' champ.txt 
```
- to print only the line which has soc 

```shell

awk '/soc/ {print}' employee.txt 

```
**Splitting a Line Into Fields :**

For each record i.e line, the awk command splits the record delimited by whitespace character by default and stores it in the $n variables. 
If the line has 4 words, it will be stored in $1, $2, $3 and $4 respectively. Also, $0 represents the whole line.  

```bash
awk '{print $1,$4}' employee.txt 


pulka  45000
hinata  25000
shruthi 100000
varun   50000
pulka  45000
binod   25000
Alle  100000
kandu   50000
```
**stuck ???**
let me clarify this assume you have line like below 
```md
iam a noob hacker
$1  $2 $3   $4

awk {print $1,$4}

output = iam hacker
```
the awk treates line a context like above 

# Conclusion


In this guide, we covered some basic text manipulation tasks using Linux commands. These techniques can be useful for various tasks such as data extraction, manipulation, and cleaning in scripting and automation workflows. By mastering these commands, you can efficiently work with text data in Linux environments
I know i didn't cover full topic i will update again this blog lately `:)` hope u enjoyed the blog 
