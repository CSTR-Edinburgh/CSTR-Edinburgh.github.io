---
layout: post
title: Vector representations based on acoustic counts
author: Sam Ribeiro
---

This paper presents a simple count-based approach to learning word vector representations by leveraging statistics 
of co-occurrences between text and speech. 
This type of representation requires two discrete sequences of units defined across modalities. 
Two possible methods for the discretization of an acoustic signal are presented: a cluster-based and a mean-based approach. 
These are then applied to the fundamental frequency and energy contours of a transcribed corpus of speech, 
yielding a sequence of textual objects (e.g. words, syllables) aligned with a sequence of discrete acoustic events. 

Constructing a matrix recording the co-occurrence of textual objects with acoustic events and reducing its dimensionality 
with matrix decomposition results in a set of context-independent representations of word types. 
These are applied to the task of acoustic modelling for speech synthesis; 
objective and subjective results indicate that these representations are useful for the generation of acoustic parameters 
in a text-to-speech (TTS) system. 

In general, we observe that the more discretization approaches, acoustic signals, 
and levels of linguistic analysis are incorporated into a TTS system via these count-based representations, 
the better that TTS system performs.

In the figure below, the co-occurrence count matrix is populated by taking counts of acoustic
classes *C* and textual objects such as words. 
This example uses a window of size *w = 3*. 
For all instances of the word token house, we take counts of the co-occurring acoustic event *c_j* and its neighboring events *c_i* and *c_k* . 
Note that the word tokens co-occurring with *house* do not participate in the count vectors.
Only the co-occurring acoustic tokens.
Each of the 3 sub-vectors of house is then normalized by the total number of counts.
We then reduce the dimensionality of the normalized count matrix by finding the Singular Value Decomposition
(SVD) of the matrix and taking the top left singular vectors.

![co-occurence matrix example]({{ site.baseurl }}/images/2017-06-06-count-representations.png
"co-occurence matrix")

Further details can be found in the paper:
* Ribeiro, M.S., Watts, O., and Yamagishi, J. (2017) [Learning word vector representations based on acoustic counts](http://homepages.inf.ed.ac.uk/s1250520/docs/ribeiro-et-al-interspeech17.pdf), In Proc. Interspeech. Stockholm, Sweden. August 2017. *To Appear*.
