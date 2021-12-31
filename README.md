# Visual-neuroscience-rig-documentation


# Hardware overview
a)	Pco Panda.  This camera comes with a USB 3.1 card.

b)	Light source. We use the Excite 110LED, which communicates with MATLAB SDK code in [widefield-imaging](https://github.com/inauhaus/widefield-imaging). But any light sournce can be manually operated without any modifications to the code.  

c)	Optical filters for reflectance (e.g. intrinsic hemodynamic) or fluorescence (e.g. GCaMP) imaging.*

d)	TTL output synchronized to visual stimuli, which triggers frame grabs at the camera. We use the 1208FS from Measurement Computing.  It is has a USB connection to 'computer B' and is controlled by Psychtoolbox.

e)	'Computer A' for GUI control and image acquisition.  We use a Windows PC.  This machine should have at least 32 GB of RAM and have Matlab 2021.  See other specs from Pco. This machine should point to the files in [visual-stimulus-controller](https://github.com/inauhaus/visual-stimulus-controller) and [widefield-imaging](https://github.com/inauhaus/widefield-imaging). 

f)  'Computer B' receives remote commands to generate visual stimuli. We are using Mac OS Catalina.  See Psychtoolbox for MATLAB and OS compatibility. This machine should point to the files in [visual-stimulus-generator](https://github.com/inauhaus/visual-stimulus-generator).  

g)  Two-photon microscope (optional).  We use a Neurolabware scope and acquisition software by Scanbox.  The data analysis GUI assumes their data struture.

h)  'Computer C' is required if two-photon imaging is used. This machine should point to the files in [2-photon-analysis](https://github.com/inauhaus/2-photon-analysis). 

*This document does not discuss the optics or illumination setup. It focuses on setting up the software for visual stimuli, image acquisition, and analysis.



SCHEMATIC OF CONNECTIVITY:

To perform widefield imaging alone, only computer 'A' and 'B' are used.  For two-photon acquisition, a third machine ('C') is necessary.

![Slide1](https://user-images.githubusercontent.com/13107530/145627782-aee2ca0b-4889-453e-992b-73eba64d8565.jpeg)

# [visual-stimulus-controller](https://github.com/inauhaus/visual-stimulus-controller)
This code sends commands over udp to a computer that presents visual stimuli (see visual-stimulus-generator repo). It also aligns experimental information (e.g. file names) with local widefield, local ephys, or remote 2photon acquisition. Visual stimulus parameters are configured using MATLAB GUI in this folder.  It is used on a Windows 10 machine with MATLAB 2021.

Install:

1) Download all files in this repo to the same root folder.
2) Set your Matlab path to this root folder. Do not set paths to deeper folders.
3) In Stimulator.m, change 'root_controller' to be the same as this root folder.
4) If you are using widefield analysis code, change root_WFanalysis to the location of that code. 
5) Create a folder that will store the .analyzer files, which contain all the experiment information files.  We call this folder /AnalyzerFiles/.  

configureMstate.m: 

Here, you will set folder locations, ip addresses, some flags, and a few other high level defaults. For example, 'Mstate.analyzerRoot' is the folder you created for the .analyzer files above.  ip addresses are for the visual stimulus computer (see visual-stimulus-generator repo), along with the 2p computer if you happen to be doing that (Ringach's Scanbox in our case).

You can also include display defaults, such as monitor distance and type. Each monitor used at this rig should have a string identifier, such as "LCD1".  By setting the monitor, it will assume certain screen dimensions and gamma calibration. These settings can be adjusted in the GUI as well.


# [visual-stimulus-generator](https://github.com/inauhaus/visual-stimulus-generator)

This code is called from 'computer B' and generates the visual stimuli using Psychtoolbox. It receives commands from [visual-stimulus-controller](https://github.com/inauhaus/visual-stimulus-controller).

Install:
1) Install Psychtoolbox
2) Download all files in this repo to the same root folder.
3) Set your Matlab path to this root folder and all of the folders inside it.
4) Hard code changes in the following files

  configCom.m:
Change the ip address to that of 'computer A'.

  configureMstate.m
For a quick start, set Mstate.monitor to 'LIN', which stands for linear. It will not access a calibration file.  The other monitor display strings are shown in updateMonitor.m.

  updateMonitor.m:
Under each monitor 'case', you will provide the file location of your gamma calibration.  You will also define the size of each     display case (cm).  The 'LIN' case is used when you don't have a calibration yet, or don't want to use one (e.g. while calibrating). The desired monitor in your lab (e.g. "LCD", etc.) is set remotely in the visual-stimulus-controller GUI. Some examples of different monitors from our lab are shown as the different cases.

# [widefield-imaging](https://github.com/inauhaus/widefield-imaging)

There are two GUIs. One to collect widefield imaging data, and one to analyze it. It runs on the same computer as [visual-stimulus-controller](https://github.com/inauhaus/visual-stimulus-controller)

# [2-photon-analysis](https://github.com/inauhaus/2-photon-analysis)
This code runs a Matlab GUI for analyzing visual responses recorded from a two-photon microscope. The microscope and acquisition software is from [Neurolabware](http://neurolabware.com/) and [Scanbox](https://scanbox.org/tag/ringach/). 


