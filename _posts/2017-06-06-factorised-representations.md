---
layout: post
title: Factorised representations for neural network adaptation to diverse acoustic environments
author: Joachim Fainberg
---

Adapting acoustic models jointly to both speaker and environment has been shown to be effective. In many realistic scenarios, however, either the speaker or environment at test time might be unknown, or there may be insufﬁcient data to learn a joint transform. Generating independent speaker and environment transforms improves the match of an acoustic model to unseen combinations. Using i-vectors, we demonstrate that it is possible to factorise speaker or environment information using multi-condition training with neural networks.

Speciﬁcally, we extract bottleneck features from networks trained to classify either speakers or environments. We perform experiments on the Wall Street Journal corpus combined with environment noise from the Diverse Environments Multichannel Acoustic Noise Database. Using the factorised i-vectors we show improvements in word error rates on perturbed versions of the eval92 and dev93 test sets, both when one factor is missing and when the factors are seen but not in the desired combination.

The figure below demonstrates the effect of factorising speaker i-vectors. The coloured clusters on the left indicate environments. By extracting bottleneck features from a network learned to classify speakers given i-vectors, the knowledge of environments is largely factored out (right).

![t-SNE of bottleneck features]({{ site.baseurl }}/images/2017-06-06-factorised_ivectors.png
" t-SNE visualisation of i-vectors before and after factorisation.")

Further details can be found in the paper:
- Fainberg, J., Renals, S., Bell, P. (2017) [Factorised representations for neural network adaptation to diverse acoustic environments](http://homepages.inf.ed.ac.uk/s1043206/papers/is-2017.pdf), In Proc. Interspeech. Stockholm, Sweden. August 2017. *To appear*.
