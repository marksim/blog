---
layout: post
title: "Adventures in Elixir"
date: 2013-08-05 09:59
comments: true
categories: blog elixir functional
---

At the [Lone Star Ruby Conference](http://lonestarruby.org/), Dave Thomas talked about [Elixir](http://elixir-lang.org) to everyone.  I found it kindof interesting that there were no loops and the use of <code>if</code> was discouraged.  It was neat to see that everything was idempotent and that pattern matching made certain problems incredibly easy to solve with very little code.

So when I found [exercism.io](http://exercism.io/) and saw that they had an Elixir track, I jumped on it. What I've noticed is that solving problems in a functional way changes the way that I code in an OO language.  It doesn't mean I want everything to be a function and never have state, but I want each method on an object to have no side effects and to require an absolute minimum of internal state to function.  

Let's look at some examples from the [Exercism](http://exercism.io) Elixir track.

### Pattern Matching

The Fibonacci sequence is an oft-asked puzzle question since it requires knowledge of recursion and proper branching conditions.  In Elixir, it breaks down very simply because of pattern matching.

``` elixir fib.exs
defmodule Fib do
  def fib(0), do: 0
  def fib(1), do: 1
  def fib(n), do: fib(n-1) + fib(n-2)
end
```

Since Elixir looks for the first match when a function is called, <code>Fib.fib(1)</code> matches line 3, and <code>Fib.fib(2)</code> matches line 4, which calls <code>fib(1) + fib(0)</code> which then match lines 2 and 3.  Impressive, no?

### Guards

Guards allow you to pattern match based on a property of the values being passed to the function.  This lets you test the types without having to have branches inside your function.  There are only [a few expressions that can be used as guards](https://gist.github.com/marksim/6156871).   

``` elixir dna.exs
defmodule DNA do
  def to_rna(strand) when is_binary(strand) do
    String.replace(strand, "T", "U")
  end

  def to_rna(strand) when is_list(strand) do
    to_rna(list_to_binary(strand)) |> to_char_list
  end
end
```

This allows you to have a single interface for Lists, Binarys, Bitstrings and Tuples, even if the logic for each one is quite different.  Since they're all separated, it becomes very easy to maintain..

### Cond

Cond is an interesting construct, similar to case, but without an initial argument.  It is more like saying <code>case true ...</code>.  As a result, it's very easy to pattern match on anything.

``` elixir bob.exs
def hey(string) do
  cond do
    is_silent?(string) ->
      "Fine. Be that way."
    is_asking?(string) ->
      "Sure."
    is_shouting?(string) ->
      "Woah, chill out!"
    true ->
      "Whatever."
  end
end
```

### Pipelining

Since it's really common to work on the result of one function in another function, but you don't have objects which keep internal state, Elixir and Erlang have the idea of pipelining.

``` elixir word-count.exs
defmodule Words do
  def count(sentence) do
    sentence |> normalize |> find_words |> count_words
  end

  defp count_words(words) do
    Enum.reduce(words, HashDict.new, fn(word, dict) ->
      HashDict.update(dict, word, 1, &1 + 1)
    end)
  end

  defp find_words(sentence) do
    Regex.scan(%r/\w+/, sentence)
  end

  defp normalize(string) do
    String.downcase(string)
  end
end
```

Pipelining is really just a shorthand for passing the result of one function in as the first argument for the next function.  As you can see on line 3, this makes it very easy to read the order in which you would think of things.  "Take a sentence, normalize it, find the words in it, count the words you found.".  The other way to write this would be <code>count_words(find_words(normalize(sentence)))</code>.  It works, but it's harder to read and you end up with [lots of right-parens](http://stackoverflow.com/a/235790/13968).

While there's nothing super special about this, I have found it very useful for readability, and that's a huge part of programming.

### Binarys, Strings and Lists - Oh My.

One of the most confusing things about Elixir (and Erlang) when I started off is that `'abc'` != `"abc"` because one is a list of characters (i.e. `[A?, B?, C?]`) and one is a UTF8 binary (i.e. `<<65, 66, 67>>`).

You can convert one into the other, though, if you are trying to work that way:

``` elixir convert.exs
# 'ABC' to "ABC"
list_to_binary('ABC') # => "ABC"

# "ABC" to 'ABC'
to_char_list("ABC") # => 'ABC'
```

But the best thing to do is to think of them as two very separate things.  If you're working with Strings, you're really working with UTF8 encoded binaries.  If there are valid UTF8 codes contained inside the binary, you'll get a string returned.  If not, you'll get a generic binary.  Understanding this difference is crucial for working with Strings in Elixir, especially when coming from another language like Ruby.

### The Documentation

Lastly, I learned how to find things in the documentation.  Understanding how the standard library works is key to being effective in any language, and the [available docs](http://elixir-lang.org/docs/stable/) are okay.  They're not great though.  Lots of holes and sometimes it's difficult to understand exactly what an argument does.  

### Concurrency

This is the key part of Elixir and I have to admit that I know very little about it.  I intend to explore it more as I go forward and hopefully write another post outlinging what I've learned.

### Going forward

Elixir is a neat langauge.  I think it will do more to influence developers in other languages than it will become a production ready system, but either way, it has taught me a handful of ideas that make me consider what advantages functional programming has and how I can incorporate them into my day to day work.  Looking foward to diving in more.
