---
layout: common
title: Answer
---
Macros perform textual manipulation, and thus act as a "preprocessor" for input files.  When the syntax `@hello world` is encountered, the `hello` macro runs when you `load` the file, not when you call `test`.  The `hello` macro contains an explicit set of instructions, which are executed when the macro runs, and `hello` does not return an expression.  Thus, the function body of `test` is empty!
