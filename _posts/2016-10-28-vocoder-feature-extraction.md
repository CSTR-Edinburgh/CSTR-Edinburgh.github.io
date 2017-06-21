---
layout: post
title: How to extract acoustic features for Merlin using WORLD vocoder
author: Srikanth Ronanki
---

Merlin is a toolkit for building Deep Neural Network models for statistical parametric speech synthesis. 
It must be used in combination with a front-end text processor (e.g., Festival) and a vocoder (e.g., STRAIGHT or WORLD).

To build your own voice, one would require acoustic features derived from a vocoder. 
These acoustic features are further processed and used as target features for training the acoustic model. 

This post gives detailed instructions on how to extract acoustic features for Merlin using WORLD vocoder. 

Scripts
-------
Go to [misc scripts](https://github.com/CSTR-Edinburgh/merlin/tree/master/misc/scripts/vocoder/world) of world vocoder in Merlin.

You can find two types of scripts:
1. [copy-synthesis](https://github.com/CSTR-Edinburgh/merlin/blob/master/misc/scripts/vocoder/world/copy_synthesis.sh): 
This script is used first to validate the extracted acoustic features, by reconstructing the waveform.
2. [Feature extraction](https://github.com/CSTR-Edinburgh/merlin/blob/master/misc/scripts/vocoder/world/extract_features_for_merlin.sh): 
This script is used to extract the acoustic features for Merlin

Copy-synthesis
--------------
- Set the path to your own audio directory against the variable wav_dir
- Set the path to output feature directory against the variable out_dir
- Set sampling frequency (fs)

#### Run the script
    $ bash copy_synthesis.sh

If you are able to reconstruct the waveforms, you are good to go and run the next step. 

Feature extraction
------------------
- Set the path to your own audio directory against the variable wav_dir
- Set the path to output feature directory against the variable out_dir
- Set sampling frequency (fs)

#### Run the script
    $ bash extract_features_for_merlin.sh
    
Alternatively, you can use the [python script](https://github.com/CSTR-Edinburgh/merlin/blob/master/misc/scripts/vocoder/world/extract_features_for_merlin.py) 
as well for the extraction of acoustic features.     

