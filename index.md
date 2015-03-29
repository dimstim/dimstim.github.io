---
layout: index
#title: page title
#tagline: page tagline
---

dimstim is the custom written, open source, cross-platform, visual stimulus software used by
the [Swindale lab](http://swindale.ecc.ubc.ca). It's written in [Python](http://python.org)
and uses [Andrew Straw](https://github.com/astraw)'s [Vision Egg](http://visionegg.org) visual
stimulus library. Vision Egg itself does all drawing to screen via
[OpenGL](http://opengl.org|OpenGL).

dimstim has precise frame-by-frame control of what happens on screen, and has been tested on
200 Hz monitors with 5 ms frame times. It allows for permutation and covariation of a wide
variety of stimulus parameters, depending on stimulus type. Stimulus types include blank
screen, flashed and drifing bars and gratings, manually controlled bars and gratings,
artificial and [natural scene movies](http://swindale.ecc.ubc.ca/movies), and sparse noise.
Stimulus parameters include spatial location, orientation, speed, duration, size, contrast,
brightness, and spatial and temporal frequencies. Spatial parameters are specified in degrees
of spatial angle, given the distance to the screen.

Stimulus parameters are communicated on a frame-by-frame basis to an acquisition computer via
a [Data Translation](http://datatranslation.com) digital output board, for simultaneous
recording of stimulus timing and neuronal responses.

Note that dimstim has only been thoroughly tested in 32-bit Windows XP. It should run in other
operating systems, but it may not run with quite the same degree of temporal accuracy.

dimstim is described in the paper [Python for large-scale
electrophysiology](http://www.frontiersin.org/Neuroinformatics/10.3389/neuro.11.009.2008/abstract).

Download
========

dimstim is available in its own [GitHub repository](https://github.com/dimstim/dimstim).

Example movie
=============

Here is an example [natural scene movie](http://swindale.ecc.ubc.ca/movies) which was
converted to greyscale for use in dimstim.

Example script
==============

Here is an example dimstim Python script for a drifting grating experiment:

```python
# Static parameters remain constant during the experiment
s = StaticParams()
# pre-experiment duration to display blank screen (sec)
s.preexpSec = 1
# post-experiment duration to display blank screen (sec)
s.postexpSec = 1
# x coord of stimulus center relative to screen center (deg)
s.xorigDeg = dc.get("Manbar0", "xorigDeg")
# y coord of stimulus center relative to screen center (deg)
s.yorigDeg = dc.get("Manbar0", "yorigDeg")

# Dynamic parameters may vary from one sweep to the next
d = DynamicParams()
# grating orientation (deg)
d.ori = range(0, 360, 30)
# spatial frequency (cycles/deg)
d.sfreqCycDeg = [0.05, 0.1, 0.2, 0.4, 0.8, 1.6]
# temporal frequency (cycles/sec)
d.tfreqCycSec = [0.5, 1, 2, 5]
# grating phase to begin each sweep with (+/- deg)
d.phase0 = 0
# mean luminance (0-1)
d.ml = 0.5
# contrast (0-1), >> 1 gives square grating, < 0 reverses contrast
d.contrast = 1
# sweep duration (sec)
d.sweepSec = 6

# Assign dynamic parameters to stimulus dimensions
vs = Variables()
vs.ori = Variable(vals=d.ori, dim=0, shuffle=True) # dim is dimension number
vs.sfreqCycDeg = Variable(vals=d.sfreqCycDeg, dim=1, shuffle=True)
vs.tfreqCycSec = Variable(vals=d.tfreqCycSec, dim=2, shuffle=True)

runs = Runs(n=1, reshuffle=False) # run parameter combinations n times
bs = BlankSweeps(T=20, sec=2) # blank sweep every T sweeps for sec seconds
e = Grating(script=__file__, static=s, dynamic=d, variables=vs,
            runs=runs, blanksweeps=bs) # create a Grating experiment
e.run() # run the experiment
```

In this example, grating orientation, spatial and temporal frequency are the only 3 parameters
assigned multiple values, and therefore the only ones to vary from one stimulus "sweep" (6 sec
in duration) to the next. Each varies independently because each is set to a different
dimension (second code block from bottom). This script can be modified into a flashed grating
experiment by setting the temporal frequency (`tfreqCycSec`) to 0, setting the phase
(`phase0`) to a range of values in degrees, and decreasing the sweep duration (`sweepSec`).
The stimulus is centered on-screen according to the position previously set by a manually
controlled oriented bar (`"Manbar0"`) stimulus. Some initialization code and stimulus
parameters are omitted for brevity. Comments are preceded by a `#`. More example scripts, one
for each stimulus type, can be found in the
[examples](https://github.com/dimstim/dimstim/tree/master/examples) folder.
