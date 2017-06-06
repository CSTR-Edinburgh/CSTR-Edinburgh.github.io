---
layout: post
title: Sequence-to-sequence models for punctuated transcription combining lexical and acoustic features
author: Ondrej Klejch
---

In this paper we present an extension of our previously described neural machine translation based system for punctuated
transcription. This extension allows the system to map from per frame acoustic features to word level representations
by replacing the traditional encoder in the encoder-decoder architecture with a hierarchical encoder. Furthermore, we
show that a system combining lexical and acoustic features significantly outperforms systems using only a single source
of features on all measured punctuation marks. The combination of lexical and acoustic features achieves a significant
improvement in F-Measure of 1.5 absolute over the purely lexical neural machine translation based system.

![Hierarchical encoder]({{ site.baseurl }}/images/2017-3-9-hierarchical-encoder.png
" Illustration of a hierarchical encoder encoding per frame acoustic features to word level features.")

Further details can be found in the paper:
* Klejch, O., Bell, P., and Renals, S. (2017) [Sequence-to-sequence models for punctuated transcription combining lexical and acoustic features](http://homepages.inf.ed.ac.uk/s1569734/papers/icassp-2017.pdf), In Proc. ICASSP. New Orleans, USA. March 2017.
