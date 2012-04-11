---
layout: common
title: Answer
---
    macro hello(ex)
        :(println(strcat("Hello ", $ex)))
    end

    function test(w)
        @hello w
    end

The first could alternately be written
    macro hello(ex)
        quote
            println(strcat("Hello ", $ex))
        end
    end


The difference between this version and the previous one is that the `hello` macro returns an expression.  Thus, when you execute `load("mhelloworld2.jl")`, the line `@hello w` in `test` is replaced with `println(strcat("Hello ",w))`.
