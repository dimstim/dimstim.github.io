---
layout: index
#title: page title
#tagline: page tagline
---

dimstim is the custom written, open source, cross-platform, visual stimulus software used by
the [Swindale lab](http://swindale.ecc.ubc.ca). It's written in [Python](http://python.org)
and uses [Andrew Straw](https://github.com/astraw)'s [Vision Egg](http://visionegg.org) Python
graphics library. Vision Egg itself does all drawing to screen via
[OpenGL](http://opengl.org|OpenGL).

dimstim has precise frame-by-frame control of what happens on screen, and has been tested on
200 Hz monitors with 5 ms frame times. It allows for permutation and covariation of a wide
variety of stimulus parameters, depending on stimulus type. Stimuli include manual and
drifting bars and gratings, flashed bars and gratings, sparse noise, and artificial and
[natural scene movies](http://swindale.ecc.ubc.ca/movies). Stimulus parameters include spatial
location, orientation, speed, duration, size, contrast, brightness, and spatial and temporal
frequencies. Spatial parameters are specified in degrees of spatial angle, given the distance
to the screen.

Stimulus parameters are communicated on a frame-by-frame basis to an acquisition computer via
a [Data Translation](http://datatranslation.com) digital output board, for simultaneous
recording of stimulus timing and neuronal responses.

Note that recent versions have only been tested in Windows. They should be possible to run in
other OSes, but perhaps not with the same degree of temporal accuracy.

dimstim is described in the paper [Python for large-scale
electrophysiology](http://www.frontiersin.org/Neuroinformatics/10.3389/neuro.11.009.2008/abstract).

Download
========

dimstim is now available in its own [GitHub repository](https://github.com/dimstim/dimstim).

Example movie
=============

Here is an example [natural scene movie](http://swindale.ecc.ubc.ca/movies) which was
converted to greyscale for use in dimstim.

Example script
==============

An example dimstim script with a description will be posted here soon.
