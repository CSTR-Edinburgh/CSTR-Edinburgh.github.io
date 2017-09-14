---
layout: post
title: Festival unit selection voice
author: Srikanth Ronanki
---

Festival offers a general framework for building speech synthesis systems as well as including examples of various modules. Multisyn is an open-source toolkit for building unit selection voice with any speech corpus. This post gives detailed instructions on how to use Multisyn to build an unit selection model and Festival for final waveform synthesis. 

## Tools required

1. [Speech tools](http://www.cstr.ed.ac.uk/projects/speech_tools)
2. [Festival](http://www.cstr.ed.ac.uk/projects/festival)
3. [Multisyn](http://www.cstr.ed.ac.uk/downloads/festival/multisyn_build)
4. [HTK](http://htk.eng.cam.ac.uk)

To build a new voice with Festival Multisyn, follow the step-by-step procedure given below:

## Step-by-step procedure

### 1. Install tools

You might be familiar with most of these tools, but there are some differences in the way we setup these tools. 

- A version of [speech tools](http://www.cstr.ed.ac.uk/downloads/festival/2.4/speech_tools-2.4-with-wrappers.tar.gz) with python wrappers has to be installed in order to work with Multisyn.
- Latest version of [Festival](http://104.131.174.95/downloads/tools/festival-2.4-current.tar.gz) has to be installed in order to use hybrid unit selection. 

Therefore, we recommend installing a fresh copy of these tools following the [scripts provided in Merlin](https://github.com/CSTR-Edinburgh/merlin/blob/master/tools/compile_unit_selection_tools.sh). 

To install speech tools, Festival and Multisyn:

```bash
bash compile_unit_selection_tools.sh
```

To install HTK:

```bash
bash compile_htk.sh
```

Make sure you install all these tools without any errors and check environment variables before proceeding further. 

### 2. setup

At this point, make sure you have data ready:

- a [directory containing audio files](http://festvox.org/cmu_arctic/cmu_arctic/cmu_us_awb_arctic/wav/) with file extension `.wav` 
- a [text file](http://festvox.org/cmu_arctic/cmu_arctic/cmu_us_awb_arctic/etc/txt.done.data) with transcriptions in the typical festival format.

For demo purpose, we use [AWB corpus from CMU Arctic Corpus](http://festvox.org/cmu_arctic/cmu_arctic/packed/cmu_us_awb_arctic-0.95-release.zip). 

Let's setup a directory for model building:

```bash
mkdir cstr_edi_awb_multisyn
cd cstr_edi_awb_multisyn
source $MULTISYN_BUILD/multisyn_build.sh
$MULTISYN_BUILD/bin/setup
$MULTISYN_BUILD/bin/setup_alignment
```

### 3. Prepare initial labels

We'll be using unilex lexicon to prepare labels which can be freely obtained by signing a license from [here](http://www.cstr.ed.ac.uk/projects/unisyn).

```bash
$MULTISYN_BUILD/bin/make_initial_phone_labs utts.data utts.mlf unilex-rpx postlex_rules my_lexicon.scm
```

### 4. Add noise

```bash
$MULTISYN_BUILD/bin/add_noise wav utts.data
```

### 5. Prepare MFCC

```bash
$MULTISYN_BUILD/bin/make_mfccs alignment wav utts.data
```

### 6. Force-alignment

```bash
cd alignment
$MULTISYN_BUILD/bin/make_mfcc_list  ../utts.data train.scp ../mfcc
ln -s ../utts.mlf aligned.0.mlf
$MULTISYN_BUILD/bin/do_alignment .
cd..
$MULTISYN_BUILD/bin/break_mlf alignment/aligned.4.mlf lab
```

### 7. Extract pitchmarks 

```bash
$MULTISYN_BUILD/bin/make_pm_wave -f pm wav utts.data
$MULTISYN_BUILD/bin/make_pm_fix pm utts.data
```

### 8. Find power factors

```bash
$MULTISYN_BUILD/bin/find_powerfactors lab utts.data
$MULTISYN_BUILD/bin/make_wav_powernorm wav_fn wav utts.data
```

Repeat steps 4-8 with normalized audio files `wav_fn`

### 9. Mark bad energy phones

```bash
$MULTISYN_BUILD/bin/make_frame_ene utts.data
$MULTISYN_BUILD/bin/Get_lr_ene utts.data
$MULTISYN_BUILD/bin/Flag_bad_energy utts.data
```

### 10. Calculate duration

```bash
$MULTISYN_BUILD/bin/phone_lengths dur lab utts.data
```

### 11. Build utts

```bash
$MULTISYN_BUILD/bin/build_utts utts.data unilex-rpx postlex_rules
```

### 12. Final alignment

```bash
cd alignment
$MULTISYN_BUILD/bin/do_final_alignment ../utts.data unilex-rpx ../postlex_rules n
cd ..
```

### 13. Compute F0

```bash
$MULTISYN_BUILD/bin/make_f0 -f wav_fn utts.data
```

### 14. Prepare coefs

```bash
$MULTISYN_BUILD/bin/make_norm_join_cost_coefs coef f0 mfcc utts.data
$MULTISYN_BUILD/bin/strip_join_cost_coefs coef coef_stripped utt utts.data
```

### 15. Prepare lpc

```bash
$MULTISYN_BUILD/bin/make_lpc wav utts.data  ## as LPC extraction code does internal normalization
```

## Build unit-selection model

Setup voice directory in Festival:
```bash
mkdir $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn
mkdir $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb
mkdir $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/festvox
```

Copy required files into the voice directory:
```bash
cp -r wav_fn $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb/wav
cp -r coef $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb/coef 
cp -r f0 $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb/f0
cp -r pm $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb/pm
cp -r utt $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb/utt
cp -r utts.data $FESTDIR/lib/voices/english/cstr_edi_awb_multisyn/awb/utts.data
```

Copy pauses from `multisyn_build/resources/pauses` into the respective directories e.g.,
```bash
cp -r awb_pauses.data $FESTDIR/lib/voices/unilex/cstr_edi_awb_multisyn/awb/
```

## Synthesis with Festival

```bash
$FESTDIR/bin/festival
```

Make festival speak "Hello world!" with new voice:

```bash
festival> (voice_cstr_edi_awb_multisyn)
festival> (SayText "Hello world!")
festival> (utt.save.wave (utt.synth (Utterance Text "Hello world!" )) "hello_world.wav")
```
