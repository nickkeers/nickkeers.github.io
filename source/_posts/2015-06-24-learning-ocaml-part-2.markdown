---
layout: post
title: "Learning OCaml - Part 2"
date: 2015-06-24 13:58:01 +0100
comments: true
categories: ['OCaml', 'Walkthrough']
---

Day 2 of the learning process! Today I’ve changed the way I’m writing, I’m now writing the tutorial as I’m learning, which should make everything easier to understand – the last post was a mix of tenses and wasn’t very clear in my opinion. I’ve also switched to writing the tutorial locally using a WYSIWYG editor called Blue Griffon (http://bluegriffon.org/), this is still not ideal as the process of adding code tags and hyperlinks etc is slow because of the lack of keyboard shortcuts; but the generated HTML it produces is very tidy.
<!--more-->

## Onto the learning!

So, in part 1 I setup the latest version of OCaml and Opam for managing packages, now we can get to playing with the syntax. OCaml supports a REPL which is always helpful when you’re learning or just wanting to try out something quickly. The REPL can be started with ocaml options objects for interactive mode – I ran ocaml to start.

And so time to play around with some things, I’m going to use the OCaml basics tutorial as a reference.

So, looking through the first lines I can see multi-line comments are in the form:
``` ocaml
(*

A multiline comment

*)
```
And there are no single line comments, well, guess I can live with that. The basics tutorial then goes into defining functions, but I think that’s going a bit too far forward, instead I’m going to look around for something that describes OCaml types and operators as I know there are different operators depending on the data types used.

## Types

I searched for “OCaml primitive data types” and found this helpful page: http://www2.lib.uchicago.edu/keith/ocaml-class/data.html – excellent, it lists all the primitive types. Looks like as far as primitives there are:

- Integers
- Floating point
- Characters
- Booleans
- Unit values – for functions that return no value – I’m familiar with
these through Haskell
- Tuples
- Lists
- Arrays
- Option – optional values, I like how this is included in the standard
library, very helpful.
- Records
- References
- Variants – user-defined types
- Objects
- Functions
- Exceptions
- Formats (for printf) – how odd.

Wow, that’s a lot. Luckily most of these are familiar to me due to previous experience whichis great.
Operators

I did another search here for “OCaml operators” and found another website: http://caml.inria.fr/pub/docs/manual-ocaml/expr.html#sec138 Scrolling down reveals a table of operators and their meaning, that’s helpful. And yep, there we go, looks like there are different operators for floating point and integers.

Back to the REPL to try some of them out. Some basic integer expressions, result after the terminating semi-colons:
``` ocaml
1 + 2;;     (* - : int = 3  *)

4 / 2;;     (* - : int = 2  *)

6 * 3;;     (* - : int = 18 *) 

~-5;;       (* - : int = -5  Representing a negative number *)

1 land 0;;  (* - : int = 0  Bitwise logical AND *)
```

Ok, well that wasn’t too bad, I like how the Bitwise logical operators are easy to remember: lor, land, lxor, etc. So let’s try some expressions that involve floating point numbers:

``` ocaml
1.0 +. 1.25;;   (* - : float = 2.25 *)

3.141592 *. (5.0 *. 5.0);;   (*  - : float = 78.5398 *)

9.831 /. 1.3451;;  (*  - : float = 7.30875027878968098 *)
(* Wow, a good amount of precision too *)
```

## Functions

Now we can look at functions! Let’s write a set of functions for computing the area of a circle. The formula for the area of a circle is ${\pi}r^{2}$ , and knowing that we can write a function that takes a radius and returns the area of the circle. Functions in OCaml according to the basics guide are in the form:

``` ocaml
let function x y = expr;;
```

So the area function would be:
``` ocaml
(*
I tried defining area like this, but it didn't work. Not too sure why yet, but we'll get back to it at some point.
let area r : float -> float = (4.0 *. atan 1.0) *. (r *. r);;
Error: This expression has type float but an expression was expected of type
         float -> float
*)
 
let pi = 4.0 *. atan 1.0;; (* extracted pi out, this is as close as you can get apparently to pi with OCaml's float *)
let area r =
  pi *. (r *. r);;

area 5;;  (* - : float = 78.5398163397448315 *)
```

Ok, we’ve covered a lot of ground. That’s the very basics of OCaml, primitive data types and basic functions. Tomorrow I’m going to plan on looking at specifying types in functions and recursion, and perhaps writing a full program that does something useful.

Sidenote: I’ve just copied in the source from the editor, and all the lines were positioned oddly, I had to manually shift lines together as there were odd breaks throughout. Looks like it’s back to the wordpress editor next time, unless anyone has a better idea?
