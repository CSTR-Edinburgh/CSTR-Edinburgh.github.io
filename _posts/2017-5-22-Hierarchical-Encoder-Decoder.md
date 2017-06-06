---
layout: post
title: A hierarchical encoder-decoder model for SPSS
author: Srikanth Ronanki
---

Current approaches to statistical parametric speech synthesis using Neural Networks generally 
require input at the same temporal resolution as the output, typically a frame every 5ms, or in some cases 
at waveform sampling rate. It is therefore necessary to fabricate highly-redundant frame-level (or sample-level) 
linguistic features at the input. 

This [paper](http://srikanthr.in/interspeech_2017_paper.pdf) 
proposes the use of a hierarchical encoder-decoder model to perform 
the sequence-to-sequence regression in a way that takes the input linguistic features at their original timescales, 
and preserves the relationships between words, syllables and phones. The proposed model is designed to make more effective 
use of supra-segmental features than conventional architectures, as well as being computationally efficient. Experiments 
were conducted on prosodically-varied audiobook material because the use of supra-segmental features is thought to be 
particularly important in this case. Both objective measures and results from subjective listening tests, which asked 
listeners to focus on prosody, show that the proposed method performs significantly better than a conventional architecture 
that requires the linguistic input to be at the acoustic frame rate.

Below is the schematic diagram of a hierarchical encoder-decoder for SPSS. The lower part of the network is the hierarchical encoder, with each layer operating at a particular linguistic level, and phone-level recurrence as its final encoded output. The upper part of the network is the decoder, generating speech parameters using frame-level recurrence. Solid black lines indicate the propagation of hidden activations between layers, and dashed colored lines indicate the injection of linguistic features at the appropriate level. The patterns of connections between word, syllable and phone layers is determined by the known linguistic structure of the current utterance. Each block of green units represents a phone, with the number of units corresponding to its duration in frames (although not drawn to scale).

![Hierarchical encoder-decoder model]({{ site.baseurl }}/images/2017-5-22-hed-encoder-decoder.png
"Schematic diagram of a hierarchical encoder-decoder for SPSS")

We'll soon provide code and a recipe to enable our system to be 
reproduced using the [Merlin toolkit](https://github.com/CSTR-Edinburgh/merlin).

Further details can be found in the paper:
* Ronanki, S., Watts, O., and King, S. (2017) [A Hierarchical Encoder-Decoder Model for Statistical Parametric Speech Synthesis](http://srikanthr.in/interspeech_2017_paper.pdf), In Proc. Interspeech. Stockholm, Sweden. August 2017. *To Appear*.

