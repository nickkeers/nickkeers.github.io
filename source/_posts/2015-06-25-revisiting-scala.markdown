---
layout: post
title: "Revisiting Scala"
date: 2015-06-25 14:25:39 +0100
comments: true
categories: scala,programming,javafx
---

I've been feeling ill the last couple of days and haven't been able to face writing, but today I'm a lot better, so that means it's time to write! I'm going to take a break from OCaml for a little bit - to tell the truth I was mostly interested in using F# and OCaml was more something to help with learning as F# and OCaml are very similar. Today I'm going to look at Scala again which should be more fun as I'm a Java programmer!
<!--more-->
## The state of Scala

As of the time of writing (25/06/2015) Scala is currently on version 2.11.7 and has come a long way since I last had a look at it. I'm mostly interested in using Scala to create GUI applications and so that's what this post will focus on. 

In Java 8 JavaFX was introduced as a replacement for the aging Swing framework. If you've worked with Swing before I'm sure you can see why a replacement is long overdue. Since I'm interested in both functional programming and GUI programming this is a perfect opportunity to try out both Scala and JavaFX (via [ScalaFX](http://www.scalafx.org/)) at the same time and learn a little about both.

## Installation

I'm not going to cover this in much depth as there are plenty of resources on the internet. I installed the latest version of Scala (2.11.7) as mentioned above, and then installed SBT. To write Scala code I'm using IntelliJ with the excellent Scala plugin.

Part of the reason for moving away from OCaml (for now anyway) was the lack of tooling - or at least tooling which would be responsive enough  (I'm looking at you eclipse) on the laptop I am currently using.

The hello world code from the ScalaFX code was useful and shows how GUI's are constructed. The code looks like this:

``` scala
package hello

import scalafx.application.JFXApp
import scalafx.application.JFXApp.PrimaryStage
import scalafx.geometry.Insets
import scalafx.scene.Scene
import scalafx.scene.effect.DropShadow
import scalafx.scene.layout.HBox
import scalafx.scene.paint.Color._
import scalafx.scene.paint.{LinearGradient, Stops}
import scalafx.scene.text.Text

object ScalaFXHelloWorld extends JFXApp {

  stage = new PrimaryStage {
    title = "ScalaFX Hello World"
    scene = new Scene {
      fill = BLACK
      content = new HBox {
        padding = Insets(20)
        content = Seq(
          new Text {
            text = "Hello "
            style = "-fx-font-size: 48pt"
            fill = new LinearGradient(
              endX = 0,
              stops = Stops(PALEGREEN, SEAGREEN))
          },
          new Text {
            text = "World!!!"
            style = "-fx-font-size: 48pt"
            fill = new LinearGradient(
              endX = 0,
              stops = Stops(CYAN, DODGERBLUE)
            )
            effect = new DropShadow {
              color = DODGERBLUE
              radius = 25
              spread = 0.25
            }
          }
        )
      }
    }
  }
}
```

The result looks like this: {% img center /images/scalafx_hello.png %}

Simple enough, right? Looks like components are even styled using CSS-like properties which is handy.

## Something more complex

Of course, it wouldn't do to learn about a GUI framework and not create a temperature converter. So let's do so!

We'll make a temperature converter which converts between degrees celcius and farenheight. 

``` scala
package hello

import scalafx.application.JFXApp
import scalafx.application.JFXApp.PrimaryStage
import scalafx.collections.ObservableBuffer
import scalafx.scene.Scene
import scalafx.scene.control.{ComboBox, Label, TextField}
import javafx.util.StringConverter

/**
 * Created by nick on 26/06/15.
 */
class TempConvert extends JFXApp
{
  def cToF(c: Double): Double = (9/5d * c) + 32
  def fToC(f: Double): Double = 5/9d * (f - 32)
  def cToF(c: String): String = cToF(c.toDouble).round.toString
  def fToC(f: String): String = fToC(f.toDouble).round.toString

  val contents = ObservableBuffer("C", "F")

  val myCombo = new ComboBox[String] {
    items = contents
  }

  val celsius = new TextField
  val fahrenheit = new TextField

  def isNumeric(s: String): Boolean = {
    try { s.toDouble }
    catch { case _: Throwable => return false }
    true
  }

  celsius.text.bindBidirectional[String](fahrenheit.text, new StringConverter[String] {
    override def fromString(c: String): String =
      if (isNumeric(c)) cToF(c) else fahrenheit.text()
    override def toString(f: String): String =
      if (isNumeric(f)) fToC(f) else celsius.text()
  })

  stage = new PrimaryStage {
    title = "Temperature Convert"

    scene = new Scene {
      content = Seq(celsius, Label("Celsius ="), fahrenheit, Label("Fahrenheit"))
    }
  }
}
```

This is mostly copy and pasted code from [7 GUI's](https://github.com/eugenkiss/7guis/blob/master/Scala-ScalaFX/src/main/scala/sevenguis/temperature/Temperature.scala), but wow, there's actually a lot going on in these 50 or so lines. The main thing to note here is the bidirectional binding between the class variables celsius and fahrenheit, when you update one textbox, the other updates too - this is going to be extremely useful!

## So, where do we go from here?

There are a couple of applications I'd like to make to learn a bit more about Scala. I'd like to make an application like [HarooPad](http://pad.haroopress.com/) which i'm using to crate new posts for this blog which is running Octopress; however I'd like the ability to parse the YAML in the header and for the GUI to be more minimal - all I want is a pane on the left for markdown and a live preview on the right.

I also play a fair amount of League of Legends, Riot Games has an official API to interact with game data and so I'd like to have a play around with this in Scala to make an application to see opponents stats or to analyse my performance in games.

I'm not sure which one would be easier to make first, or if I'd maybe have to do something smaller first. However, I feel I learn faster by having a project to complete and learning as I go - so many decisions...

That's all for now!