---
layout: post
title: Multisyn unit selection voice
author: Srikanth Ronanki
---

Multisyn is a open-source toolkit for building a new unit selection voice with any speech corpus. 

To build a new voice, follow the step-by-step procedure given below:

## Step-by-step procedure

### 1. setup

```bash
mkdir cstr_crpx_fls_multisyn
cd cstr_crpx_fls_multisyn
source $MULTISYN_BUILD/multisyn_build.sh
$MULTISYN_BUILD/bin/setup
$MULTISYN_BUILD/bin/setup_alignment
```

### 2. prepare initial labels

```bash
$MULTISYN_BUILD/bin/make_initial_phone_labs utts.data utts.mlf combilex-rpx postlex_rules my_lexicon.scm
```

### 3. add noise

```bash
$MULTISYN_BUILD/bin/add_noise wav utts.data
```

### 4. prepare MFCC

```bash
$MULTISYN_BUILD/bin/make_mfccs alignment wav utts.data
```

### 5. force-alignment

```bash
cd alignment
$MULTISYN_BUILD/bin/make_mfcc_list  ../utts.data train.scp ../mfcc
ln -s ../utts.mlf aligned.0.mlf
$MULTISYN_BUILD/bin/do_alignment .
cd..
$MULTISYN_BUILD/bin/break_mlf alignment/aligned.4.mlf lab
```

### 6. extract pitchmarks 

```bash
$MULTISYN_BUILD/bin/make_pm_wave -f pm wav utts.data
$MULTISYN_BUILD/bin/make_pm_fix pm utts.data
#$MULTISYN_BUILD/bin/make_esps_pm wav utts.data # need epochs installed - error message
```

### 7. find power factors

```bash
$MULTISYN_BUILD/bin/find_powerfactors lab utts.data
$MULTISYN_BUILD/bin/make_wav_powernorm wav_fn wav utts.data
```

Repeat steps 3-7 with normalized audio files `wav_fn`

### 8. mark bad energy phones

```bash
$MULTISYN_BUILD/bin/make_frame_ene utts.data
$MULTISYN_BUILD/bin/Get_lr_ene utts.data
$MULTISYN_BUILD/bin/Flag_bad_energy utts.data
```

### 9. calculate duration

```bash
$MULTISYN_BUILD/bin/phone_lengths dur lab utts.data
```

### 10. build utts

```bash
$MULTISYN_BUILD/bin/build_utts utts.data combilex-rpx postlex_rules
```

### 11. final alignment

```bash
cd alignment
$MULTISYN_BUILD/bin/do_final_alignment ../utts.data combilex-rpx ../postlex_rules n
cd ..
```

### 12. compute F0

```bash
$MULTISYN_BUILD/bin/make_f0 -f wav_fn utts.data
```

### 13. prepare coefs

```bash
$MULTISYN_BUILD/bin/make_norm_join_cost_coefs coef f0 mfcc utts.data
$MULTISYN_BUILD/bin/strip_join_cost_coefs coef coef_stripped utt utts.data
```

### 14. prepare lpc

```bash
$MULTISYN_BUILD/bin/make_lpc wav utts.data  ## as LPC extraction code does internal normalization
```

## Build unit-selection model

```bash
cp -r wav_fn voices/unilex/cstr_edi_fls_multisyn/fls/wav
cp -r coef voices/unilex/cstr_edi_fls_multisyn/fls/coef 
cp -r f0  voices/unilex/cstr_edi_fls_multisyn/fls/f0
cp -r pm  voices/unilex/cstr_edi_fls_multisyn/fls/pm
cp -r utt  voices/unilex/cstr_edi_fls_multisyn/fls/utt

cp -r fls_pauses.data voices/unilex/cstr_edi_fls_multisyn/fls/
cp -r utts.data voices/unilex/cstr_edi_fls_multisyn/fls/
```

## Synthesis with Festival

```bash
$FESTDIR/bin/festival
```

Make festival speak "Hello world!" with new voice:

```bash
festival> (voice_cstr_edi_fls_multisyn)
festival> (SayText "Hello world!")
festival> (utt.save.wave (utt.synth (Utterance Text "Hello world!" )) "hello_world.wav")
```
