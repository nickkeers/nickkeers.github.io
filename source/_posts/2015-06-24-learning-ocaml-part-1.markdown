---
layout: post
title: "Learning OCaml - Part 1"
date: 2015-06-24 13:57:51 +0100
comments: true
categories: ['OCaml', 'Walkthrough']
---

I’ve always been interested in learning OCaml, and I’ve been meaning to get into blogging; this means that this series (or walkthrough, as I’m going to walk you through how I’m learning as I learn) is the perfect opportunity! I’m going to attempt to write a blog post a day from now on, no matter how small the post. And so, let’s get started!
<!--more-->
## Installing OCaml

For future reference I’m running Xubuntu 15.04

To get started I opened up the OCaml website (https://ocaml.org/) and clicked the “Install OCaml” button. That button lead me to the OCaml docs. The docs told me I need to install a package manager called Opam, and so I opened a terminal and ran:

``` plain
sudo apt-get install opam
```

Now that Opam is installed I can use Opam to install the latest version of OCaml, and so I tried to run ```opam switch 4.02.2``` but was informed I need to first run ```opam init``` and so I ran that first and let Opam modify my profile and ocamlinit files.

To install OCaml I can now run ```opam switch 4.02.2``` as follows:

{% img center /images/term2.png %}

Looks like Opam is compiling OCaml from source – naturally this took a while. Opam also said m4 was needed, as many packages rely on it – who am I to argue? – I installed m4 using apt-get.

I’m glancing at the time as I’m writing this, and I’ve just realised it’s 10:46pm. The OCaml docs recommended installing packages called Batteries and Core.

I can’t seem to work out what Batteries is or does, apparently it’s a “community-driven effort to standardize on an consistent, documented, and comprehensive development platform for the OCaml programming language” – ok but that doesn’t tell me how Batteries included helps me, so I’ll skip the installation for now.

Core however seems more interesting. It looks like Core was written by the folks at Jane Street who are the largest industry users of OCaml, that means that it’s tried and tested. Core is apparently an alternative to the OCaml standard library, and I assume you don’t re-implement the standard library unless you know what you’re doing. And so, I installed Core using Opam (```opam install core```).

## Running our first OCaml program

Ok, now the fun part, lets write a program! I found it a bit difficult to find documentation on how to print a string, but I’m going to assume that’s because it’s getting late and I’m looking in the wrong places. Long story short, our hello world program is only one line:

``` ocaml
print_string "Hello world!\n";;
```

Well, that wasn’t too bad – thanks Amir Chaudhry! (http://amirchaudhry.com/ocaml-installation-and-hello-world/). I compiled the code using his instructions and it ran like a charm:

{% img center /images/opam_term.png %}

And so that’s it for tonight, tomorrow I’ll start exploring what the language itself can do by writing an example program and by running through a basic tutorial (or two!).