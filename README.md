# Visual-neuroscience-rig-documentation


# Hardware overview
a)	Pco Panda.  This camera comes with a USB 3.1 card.

b)	Light source with serial port communication to interface with 'imager' Matlab GUI.  We use the Excite 110LED, and its Matlab SDK.

c)	Optical filters for reflectance (e.g. intrinsic hemodynamic) or fluorescence (e.g. GCaMP) imaging.*

d)	TTL output synchronized to visual stimuli, which triggers frame grabs at the camera. We use the 1208FS from Measurement Computing.  It is connected with USB connection controlled with Psychtoolbox.

e)	The signals produced by ‘e’ and ‘f’ get fed into an analog-to-digital device that is connected to the acquisition PC. We use a small USB box from National Instruments (USB-9162). The analysis code compares these two signals to determine response onset.

f)	A computer for GUI control and image acquisition.  We use a Windows PC.

g)	A second computer that receives remote commands to generate visual stimuli. We use Mac OS.

h)  Two-photon microscope.  We use a Neurolabware scope and acquisition software by Scanbox.  The data analysis GUI assumes their data struture.

i). A third computer is required if two-photon imaging is used.

*This document does not discuss the optics or illumination setup.   It focuses on setting up the software for visual stimuli, image acquisition, and analysis.


# [visual-stimulus-controller](https://github.com/inauhaus/visual-stimulus-controller)
This code sends commands over udp to a computer that presents visual stimuli (see visual-stimulus-generator repo). It also aligns experimental information (e.g. file names) with local widefield, local ephys, or remote 2photon acquisition. Visual stimulus parameters are configured using MATLAB GUI in this folder.  It is used on a Windows 10 machine with MATLAB 2021.

Install:

1) Download all files to the same root folder.
2) Set your Matlab path to this root folder. Do not set paths to deeper folders.
3) In Stimulator.m, change 'root_controller' to be the same as this root folder.
4) If you are using widefield analysis code, change root_WFanalysis to the location of that code. 
5) Create a folder that will store the .analyzer files, which contain all the experiment information files.  We call this folder /AnalyzerFiles/.  

configureMstate.m: 

Here, you will set folder locations, ip addresses, some flags, and a few other high level defaults. For example, 'Mstate.analyzerRoot' is the folder you created for the .analyzer files above.  ip addresses are for the visual stimulus computer (see visual-stimulus-generator repo), along with the 2p computer if you happen to be doing that (Ringach's Scanbox in our case).


Schematic of connectivity:

To perform widefield imaging alone, only computer 'A' and 'B' are used.  For two-photon acquisition, a third machine ('C') is necessary.

![Slide1](https://user-images.githubusercontent.com/13107530/145627782-aee2ca0b-4889-453e-992b-73eba64d8565.jpeg)

# [visual-stimulus-generator](https://github.com/inauhaus/visual-stimulus-generator)

# [widefield-imaging](https://github.com/inauhaus/widefield-imaging)

# [2-photon-analysis](https://github.com/inauhaus/2-photon-analysis)


