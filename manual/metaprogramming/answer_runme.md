---
layout: common
title: Answer
---
    macro runme(ex...)
        indx = gensym()
        quote
            for $indx = 1:length($ex)
                eval(($ex)[$indx])
            end
        end
    end

By putting the evaluation statement inside a quote block, you ensure the evaluation happens at the line where the @runme appears.  Note carefully the parentheses around the `eval` statement.

After running `settest(3)`, be sure to verify that you get this:

    julia> a
    a not defined

    julia> b
    b not defined


Alternatively, @runme could be written as:

    macro runme(ex...)
        Expr(:block,Any[ex...],Any)
    end

The symbol `:block` indicates that the arguments of the expression represent a sequence of expressions.  This fact could be discovered by the following experiment:

    julia> ex = :(begin
             a = 5
             b = a+2
           end);

    julia> ex.head
    block

    julia> ex.args
    {line(2), a = 5, line(3), b = +(a,2)}

So the macro creates an expression whose `head` is `:block`.  For `args`, it converts the tuple `ex` into an array of type `Any`, as required by the definition of type `Expr`.  Finally, it sets `typ` to `Any`.  Thus, when the macro `runme` executes, it creates a line of code equivalent to `begin a=5;b=a+2; end` as the first line of the `settest` function.

