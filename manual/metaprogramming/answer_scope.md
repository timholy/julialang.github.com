---
layout: common
title: Answer
---
With `load("mscope.jl")`, the expression `a=5` is evaluated, and then the functions are parsed.  Because `a` has value 5, everywhere `a` appears it gets replaced with 5.  The function `test2`, which appears not to define `a`, simply has the body `println(5*x)`.

Note that if you type `a` from the prompt, you'll discover that it has value 5.  Macros run in the "top scope" and hence affect everything that follows.  Suppose you created another file `mscope_other.jl` with the following contents:

    function testother(x)
        println(a*x)
    end

After having already loaded `mscope.jl`, type `load("mscope_other.jl")` into the command prompt.  `a` gets replaced by 5 in this function, too.  However, if you start a fresh Julia session, load `mscope_other.jl` without first loading `mscope.jl`, and then execute `testother(9)`, naturally you get an error.
