---
layout: post
title: How to install Merlin toolkit
author: Srikanth Ronanki
---

Merlin is a toolkit for building Deep Neural Network models for statistical parametric speech synthesis. 
It must be used in combination with a front-end text processor (e.g., Festival) and a vocoder (e.g., STRAIGHT or WORLD).

This post gives detailed instructions on how to download and install Merlin toolkit on a stand-alone machine. 

Download
--------
There are two ways to download Merlin: 
- Using terminal or command-line prompt
    * git clone https://github.com/CSTR-Edinburgh/merlin.git
- Using browser
    * Go to [Merlin](https://github.com/CSTR-Edinburgh/merlin) and click _Clone or download_ button
    
Installation
------------
To install Merlin succesfully, we have to:
1. Follow the instructions in the **tools/INSTALL** file
2. Install some Python dependencies

### Step1: Install tools in Merlin
* cd merlin/tools
* ./compile_tools.sh

### Step2: Install Python dependencies
* First, let's create a directory to work:
    * mkdir ~/myproject
    * cd ~/myproject

#### Creating python virtual environment

* virtualenv \-\-distribute \-\-python=/usr/bin/python2.7 p27
* source p27/bin/activate

#### Install some tools required for _lxml_ installation

* Create a directory for tools 
    * mkdir Tools
    * cd Tools
* Download libxslt library:
    * wget ftp://xmlsoft.org/libxml2/libxslt-1.1.29.tar.gz
    * curl -L -O ftp://xmlsoft.org/libxml2/libxslt-1.1.29.tar.gz (for Mac)
* Unzip files
    * tar xvzf libxslt-1.1.29.tar.gz
    * cd libxslt-1.1.29
* Install
    * mkdir build
    * ./configure \-\-prefix=/Users/test/myproject/Tools/libxslt-1.1.29/build **(change path)**
    * make
    * make install

#### Install python libraries

* pip install numpy scipy matplotlib theano

#### export some paths to install _lxml_ and _bandmat_

* For bandmat
    * export C_INCLUDE_PATH=$C_INCLUDE_PATH:~/myproject/p27/lib/python2.7/site-packages/numpy/core/include
    
* For lxml
    * export C_INCLUDE_PATH=$C_INCLUDE_PATH:/usr/include/libxml2
    * export C_INCLUDE_PATH=$C_INCLUDE_PATH:~/myproject/Tools/libxslt-1.1.29/build/include
    * export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/myproject/Tools/libxslt-1.1.29/build/lib
    * export PATH=$PATH:~/myproject/Tools/libxslt-1.1.29/build/bin

* pip install bandmat lxml