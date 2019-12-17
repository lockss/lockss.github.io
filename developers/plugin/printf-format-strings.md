---
layout: page
title: printf Format Strings
---

*This page is under construction.*

**This page is part of the [LOCKSS Plugin Developer Manual](/developers/plugin/).**

## Definition

A **`printf` format string** is a template for generating a string of text. It consists of a **format specification** containing literal elements and **format specifiers** (placeholders with formatting hints), and a list of **expressions** for each placeholder's value.

A **`printf` interpreter** is a template engine that accepts a `printf` format string as input and produces an output string from it, based on its implementation-dependent capabilities to compute the value of expressions and on context-dependent variables.

The LOCKSS software contains a `printf` interpreter where the expressions are names of plugin configuration parameters and AU attributes, optionally modified by a small number of processing functions.

## Format

A `printf` format string consists of the following elements:

*   A **format specification**, which starts and ends with a quotation mark (`"`) and follows the `printf` specification syntax.
*   For each format specifier in the format specification, an **expression** whose value is computed and substituted for the format specifier. The successive expressions correspond to the format specifiers in the order they appear in the format specification.

These elements are comma-separated, with whitespace surrounding the elements trimmed.

Anything that is not recognized as a format specifier is interepreted to be a **literal** part of the output string.

## Format Specifiers

Format specifiers begin with a **percent sign** (`%`) and end with a **type field**, separated by optional characters further constraining the formatting of the placeholder's value. The most important type fields are:

*   **`%s`**: for **string**-valued expressions.
*   **`%d`**: for **integer**-valued expressions.
*   **`%%`**: for a **literal percent sign**.

### String

The most common format specifier is `%s` for string-valued expressions.

*Example*

```
Input:

"The base URL is %s", base_url

Output in a context where base_url is http://www.example.com/:

The base URL is http://www.example.com/
```

### Integer

The format specifier `%d` is used for an integer-valued expression.

*Example*

```
Input:
"The year is %d", year
Output in a context where year is the integer 2019:
The year is 2019
```

### Percent Sign

Because the percent sign is used to introduce format specifiers, there is type field to indicate that a placeholder is for a literal percent sign, and that type field is also the percent sign.

*Examples*

```
Input:
"100%% of the time"
Output:
100% of the time

Input:
"100% of the time"
Output will not be as intended
```

## References

*   [printf format string](https://en.wikipedia.org/wiki/Printf_format_string) on Wikipedia
