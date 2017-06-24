---
layout: post
title: Install Speech tools, Festival and Festvox
author: Srikanth Ronanki
---

Speech Tools 2.4
-----------
#### Download
    $ wget http://www.cstr.ed.ac.uk/downloads/festival/2.4/speech_tools-2.4-release.tar.gz
    $ curl -L -O http://www.cstr.ed.ac.uk/downloads/festival/2.4/speech_tools-2.4-release.tar.gz (for Mac)
    
#### Install
    $ ./configure
    $ make
    $ make install
    
#### Configure paths
    $ export ESTDIR=/path/to/speech/tools/
    $ export PATH=$ESTDIR/bin:$PATH
    $ export LD_LIBRARY_PATH=$ESTDIR/lib:$LD_LIBRARY_PATH
    
Festival 2.4
-------------

#### Download
    $ wget http://www.cstr.ed.ac.uk/downloads/festival/2.4/festival-2.4-release.tar.gz
    $ curl -L -O http://www.cstr.ed.ac.uk/downloads/festival/2.4/festival-2.4-release.tar.gz (for mac)
    
#### Install
    $ ./configure
    $ make
    $ make install
    
#### Configure paths
    $ export FESTDIR=/path/to/festival
    $ export PATH=$FESTDIR/bin:$PATH
    
#### Download lexicon and some voices    
    $ wget http://www.cstr.ed.ac.uk/downloads/festival/2.4/festlex_CMU.tar.gz
    $ wget http://www.cstr.ed.ac.uk/downloads/festival/2.4/festlex_OALD.tar.gz
    $ wget http://www.cstr.ed.ac.uk/downloads/festival/2.4/festlex_POSLEX.tar.gz
    $ wget http://festvox.org/packed/festival/2.4/voices/festvox_kallpc16k.tar.gz
    $ wget http://festvox.org/packed/festival/2.4/voices/festvox_cmu_us_slt_cg.tar.gz
    $ wget http://festvox.org/packed/festival/2.4/voices/festvox_cmu_us_awb_cg.tar.gz
