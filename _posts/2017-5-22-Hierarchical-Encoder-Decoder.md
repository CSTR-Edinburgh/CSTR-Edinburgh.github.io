---
layout: post
title: A Hierarchical Encoder-Decoder Model
---

Current approaches to statistical parametric speech synthesis using Neural Networks generally 
require input at the same temporal resolution as the output, typically a frame every 5ms, or in some cases 
at waveform sampling rate. It is therefore necessary to fabricate highly-redundant frame-level (or sample-level) 
linguistic features at the input. This [paper](http://srikanthr.in/interspeech_2017_paper.pdf) 
proposes the use of a hierarchical encoder-decoder model to perform 
the sequence-to-sequence regression in a way that takes the input linguistic features at their original timescales, 
and preserves the relationships between words, syllables and phones. The proposed model is designed to make more effective 
use of supra-segmental features than conventional architectures, as well as being computationally efficient. Experiments 
were conducted on prosodically-varied audiobook material because the use of supra-segmental features is thought to be 
particularly important in this case. Both objective measures and results from subjective listening tests, which asked 
listeners to focus on prosody, show that the proposed method performs significantly better than a conventional architecture 
that requires the linguistic input to be at the acoustic frame rate.

We'll provide code and a recipe to enable our system to be 
reproduced using the [Merlin toolkit](https://github.com/CSTR-Edinburgh/merlin).

![Hierarchical encoder-decoder model]({{ site.baseurl }}/images/2017-5-22-hed-encoder-decoder.png
"Schematic diagram of a hierarchical encoder-decoder for SPSS")

Link to paper: [http://srikanthr.in/interspeech_2017_paper.pdf](http://srikanthr.in/interspeech_2017_paper.pdf)
