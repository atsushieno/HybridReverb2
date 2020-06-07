# HybridReverb2

Binaries are at https://github.com/osxmidi/HybridReverb2/releases

For Bitwig, the vst3 needs Bitwig 3.2 or higher.

-------

To use

Initially, HybridReverb2 needs to download it's default preset file.

After that, user presets can be added by using the Preset Editor tab.

Wav IR files can be added to the preset.

To load a preset, the + and - buttons can be used in the main tab and/or double clicking on the presets name in the Preset Editor tab will quickly load that preset.

The parameter control settings in a preset can be saved using the Save button in the Preset Editor tab.

The parameter controls in a preset go to their new value after the mouse is released at a certain value or if the mouse is clicked on the parameter controls at a certain value.

Presets can be saved to an xml file (with .xml at the end of the preset file name) and preset files can be loaded.

The default startup preset file can be set in the Preferences tab.

-------

Linux make instructions

Place the unzipped HybridReverb2 folder (this download/clone) into the ~/JUCE6 folder 

There are basically 2 config options.

1: Copy the contents of the JUCE6 modules folder to the ~/JUCE6/HybridReverb2/JuceLibraryCode/modules folder (for making the default Vst3 version)

or

2: Reconfigure using Projucer.

Some files may then need to be edited
 
For Vst3, edit plugin/JuceLibraryCode/AppConfig.h 
 
and check that the below is entered
 
```
#ifndef    JUCE_VST3_CAN_REPLACE_VST2
#define JUCE_VST3_CAN_REPLACE_VST2 0
#endif 

```

To make with no Webkit, see the Webkit folder for manual config or choose the juce_gui_extra module in the Projucer and set 
 JUCE_WEB_BROWSER to Disabled.
 
Some libraries need to be installed

sudo apt-get -y install webkit2gtk-4.0 git pkg-config libfreetype6-dev libx11-dev libxinerama-dev libxrandr-dev libxcursor-dev mesa-common-dev libasound2-dev freeglut3-dev libxcomposite-dev libcurl4-gnutls-dev libfftw3-dev

To make the default Vst3 version, cd into the ~/JUCE6/HybridReverb2/Builds/LinuxMakefile folder

make CONFIG=Release

vst3 is installed into ~/.vst3

--------

The lv2 version needs JUCE lv2 from the lv2 branch at https://github.com/lv2-porting-project/JUCE

sudo apt-get install lv2-dev

Copy the contents of the JUCE modules folder to the plugin/JuceLibraryCode/modules folder 

Unzip the HybridReverb2-lv2-make.zip file in the HybridReverb2/Builds/LinuxMakefile/lv2 folder and copy the Makefile to the HybridReverb2/Builds/LinuxMakefile

cd into the HybridReverb2/Builds/LinuxMakefile folder

make CONFIG=Release

cd build

copy lv2_ttl_generator and lvmake and makelv2 (might need a chmod +x to make them executable) from the unzipped HybridReverb2-lv2-make.zip

./makelv2

--------

Reverb effect using hybrid impulse convolution

[![Build Status](https://semaphoreci.com/api/v1/jpcima/hybridreverb2/branches/master/badge.svg)](https://semaphoreci.com/jpcima/hybridreverb2)

Original author: Christian Borß  
Current maintainer: [Jean Pierre Cimalando](https://github.com/jpcima)  
Contributor: [Olivier Humbert](https://github.com/trebmuh)

The goal of this project is to keep the HybridReverb2 project maintained and fix the issues.  
All information and original source code of HybridReverb2 is available on this [project page](http://www2.ika.ruhr-uni-bochum.de/HybridReverb2/).

## Introduction

(quoted from the original project page)

> HybridReverb2 is a convolution-based reverberation effect which combines the superior sound quality of a convolution reverb with the tuning capability of a feedback delay network. The sound quality of a convolution reverb depends on the quality of the used room impulse responses. HybridReverb2 comes with a set of room impulse responses which were synthesized with tinyAVE, an auralization software which was developed at the Institute of Communication Acoustics, Ruhr-Universität Bochum (Borß and Martin, 2009; Borß, 2009a). These room impulse responses are designed for a speaker setup with two front and two rear speakers (Borß, 2009b). For a full surround sound effect, you will need two plugins, one plugin which uses a "front" preset for the front channels and a second plugin which uses the corresponding "rear" preset for the rear channels.

> Enjoy,  
Christian Borß

## Downloads

[Windows development builds](http://jpcima.sdf1.org/software/development/HybridReverb2/)

[Impulse response database](https://github.com/jpcima/HybridReverb2-impulse-response-database/archive/v1.0.0.zip) - CC-BY-SA 4.0 license

## Building

A CMake build file is provided to Linux users for the ability to build LV2 and cross-compile.  
The traditional Juce build process has build files for all platforms in the `Builds` folder. It supports all formats except LV2.

To perform a CMake-based build:

```
git submodule init
git submodule update
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
cmake --build .
```

| Build option                                  | Description                                                     |
| --------------------------------------------- | --------------------------------------------------------------- |
| -DHybridReverb2_VST2=ON/OFF                   | Build a VST2 plugin                                             |
| -DHybridReverb2_LV2=ON/OFF                    | Build a LV2 plugin                                              |
| -DHybridReverb2_Standalone=ON/OFF             | Build a standalone program                                      |
| -DHybridReverb2_AdvancedJackStandalone=ON/OFF | Build a standalone for Jack with better features                |
| -DHybridReverb2_UseLocalDatabase=ON/OFF       | Use a preinstalled RIR database in `PREFIX`/share/HybridReverb2 |
| -DHybridReverb2_Assertions=ON/OFF             | Force building with assertions regardless of build type         |

## Usage

The LV2 plugin is identified as `https://github.com/jpcima/HybridReverb2`.  
Load this in your favorite plugin hosting software. A free compatible plugin host is [Carla](https://github.com/falkTX/Carla).
