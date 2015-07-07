---
layout: post
title: "Erlang and Elixir"
date: 2015-07-03 16:08:22 +0100
comments: true
categories: erlang,elixir,programming
---


As shown by my previous posts I've been getting back into the world of functional programming after finishing my degree in Computer Science where I worked mostly in Java (plus a bit of C++ and PHP).

I still intend to keep learning Scala, however I'm currently reading through basic tutorials and a book and I don't think I'm at the point where what I write about Scala would be interesting - at least, not yet. So, let's look at something I'm more comfortable with. 
<!--more-->
In my final year dissertation I used Erlang to create a set of example sorting programs which used distributed processing on a small scale. I used four computers to implement the merge sort and bitonic sorting algorithms. 

I learnt some Erlang in the process, but it was mostly the basics; I feel as if I barely scratched the surface - however, I could tell that there was a lot that I liked about the language. Pattern matching for example is very powerful, and it makes functions that you have written extremely clear.

For example, if you wanted to write some Erlang code which computes the sum of a list we can write this:

{% codeblock lang:erlang sum.erl %}
-module(sum).
-export([sum/1]).

sum(L) ->
  sum(L, 0).

sum([H|T], N) ->
  sum(T, N + H);

sum([],N) ->
  N.
{% endcodeblock %}

We can then call run in the shell ```erl``` followed by ```c(sum).``` in the Erlang shell to compile the file (assuming you're in the same directory). From the shell you can run ```sum:sum(lists:seq(1,100)).``` which should return ```5050```. In a more traditional language such as Java you'd have to write:

{% codeblock lang:java Sum.java %}
class Sum {
    
    public static void sum(int[] numbers)
    {
        int total = 0;
        for(int n : numbers)
        {
            total += n;
        }
        System.out.println("Total: " + total);
    }
    
    public static void main(String[] args)
    {
        int[] numbers = new int[100];
        
        for(int i = 1; i <= 100; i++)
        {
            numbers[i-1] = i;
        }
        
        sum(numbers);
        
    }
}
{% endcodeblock %}

Then you could compile with ```javac Sum.java``` and run with ```java Sum``` (or you could use your preferred IDE, whichever works). That's a lot of code compared to the Erlang version, however I am aware that not everyone is a fan of functional programming.

## Onto Elixir

I decided then to look at Elixir as I feel that Erlang at times can be quite verbose. Code like in the example below is not uncommon when using Erlang:

{% codeblock lang:erlang %}
myfunction(X) ->
  funcOne(funcTwo(funcThree(X))).
{% endcodeblock %}

However, in Elixir we can write this as:

{% codeblock lang:elixir %}

def myfunction(X) do
  X 
  |> funcThree
  |> funcTwo
  |> funcOne
end

{% endcodeblock %}

The pipeline operator ```|>``` is extremely useful and helps to simplify code further, it works by feeding X into funcThree, and then the result of that into funcTwo and so on.

I then thought I'd try and write a small script that does something (vaguely) useful. I decided to write a script to list all of the files in a directory along with their file size. Here's the code:

{% codeblock lang:elixir %}
defmodule FileScan do

  def process(what) do
    IO.puts "File sizes in current directory"
    for file <- what do
      IO.puts "-------------------"
      IO.puts "File: " <> file
      {:ok, f} = :file.read_file_info(file)
      details = File.Stat.from_record(f)
      IO.puts "File size: " <> (to_string details.size ) <> " bytes"
    end
    IO.puts "-------------------"
  end

end
try do
  File.ls!(".") |> Enum.filter(fn f -> not File.dir?(f) end)
  |> FileScan.process()
rescue
  File.Error -> "Rescued file error"
  _error     -> "Rescued unknown error"
end
{% endcodeblock %}

## Wrapping up

What I really liked about this bit of code was the simplicity. When I'm writing Erlang I feel as if I have to think about every line of code I'm writing, but with Elixir I don't get that feeling. It took me a little while to understand how the File.Stat module worked, but once I understood that it was easy.

Soon I'll port this code over to Erlang for a comparison, most likely by editing this post so I'll post on Twitter when that's done. 

That's all for now. Anyone had a similar experience? Or maybe even used Elixir? If so what do you like about it - and have you got any example code you'd like to show that's relatively short?

