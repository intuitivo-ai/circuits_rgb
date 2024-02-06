# Circuits.rgb

Drive WS2812B "NeoPixel" RGB LED strips from a oRANGE Pi using Elixir!

![NeoPixel strip driven by a Raspberry Pi](nerves_neopixel_rgb.jpg)

This project was designed to make it easy to drive a string of AdaFruit NeoPixels from a oRANGE Pi using [Nerves](http://nerves-project.org).
The code would probably also work outside of Nerves with minor modifications to the Makefile, if you so desire.

Unfortunately, since the Raspberry Pi has 3.3V I/O outputs and the NeoPixels require 5V I/O input, a little piece of hardware is required.
You can read more about this in [my blog post about the project](http://www.gregmefford.com/blog/2016/01/22/driving-neopixels-with-elixir-and-nerves).

## Installation

  1. Add it to your list of dependencies in `mix.exs`:

        def deps do
          [{:circuits_rgb, "~> 2.0"}]
        end


## Usage

Supervision trees and an Elixir `Port` are used to maintain fault-tolerance when interfacing with the low-level driver, which is written in C.
To drive an NeoPixel strip, you just have to configure which GPIO pin to use and how many NeoPixels are in the strip using the `Circuits.RGB.init` function.
Once you had a `pid` from the `setup` function, you can call the `Circuits.RGB.write_rgb` function with the pid and a binary structure representing the pixel data.

Here's a simple example:

``` elixir
alias Circuits.RGB
{:ok, pid} = Circuits.RGB.init
Circuits.RGB.write_rgb(
  pid,
  24, #number led
  4567 #color
)
```

