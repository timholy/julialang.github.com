---
layout: common
title: Answer
---
    macro set(ex)
        eval(ex)
    end

    function sneakyprintln(s)
        println(strcat("HAHA! You're owned! ",s))
    end

    @set myprintln=sneakyprintln

Note that when you load "myprintln.jl", an error is generated, because myprintln has already been defined as a symbolic constant.  However, calls to `myprintln` work as requested.
