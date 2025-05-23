## sphinxtrain

The last (good) version written in C. Install [sphinxbase](https://github.com/cartheur/sphinxbase) first.

Get the 1.0.8 code [here](https://sourceforge.net/projects/cmusphinx/files/).

Read about training with `libirispeech` [here](https://cmusphinx.github.io/2022/08/sphinxtrain-librispeech/), where the website is [here](https://www.openslr.org/12/).

### What is sphinxtrain?

This is SphinxTrain, Carnegie Mellon University's open source acoustic model trainer. This directory contains the scripts and instructions necessary for building models for the CMU Sphinx Recognizer. This distribution is free software, see COPYING for licence.

For up-to-date information, please see the web site at

   https://cmusphinx.sourceforge.net

Among the interesting resources there, you will find a link to "Resources to build a recognition system", with pointers to a dictionary, audio data, acoustic model etc. For introduction in training the acoustic model see the tutorial

https://cmusphinx.sourceforge.net/wiki/tutorialam

Installation Guide:
^^^^^^^^^^^^^^^^^^^
This sections contain installation guide for various platforms. 

All Platforms:
^^^^^^^^^^^^^^
You will need Perl to use the scripts provided. Linux usually comes
with some version of Perl. If you do not have Perl installed, please
check:

http://www.perl.org

where you can download it for free. For Windows, a popular version, ActivePerl, is available from ActiveState at:

http://www.activestate.com/Products/ActivePerl/

For some advanced techniques (which are not enabled by default) you will need Python with NumPy and SciPy. Packages for NumPy and SciPy can be obtained from [here](https://scipy.org/Download).

#### Linux/Unix Installation

This distribution now uses GNU autoconf to find out basic information about your system, and should compile on most Unix and Unix-like
systems, and certainly on Linux. To build, simply run

```
    ./configure
    make
    make install
```

This should configure everything automatically. The code has been tested with `gcc`. Also, check the section title "All Platforms" above.

#### Windows Installation

First, you *must* have SphinxBase, which you can download from
http://cmusphinx.sourceforge.net/.  You should download and unpack it to
the same parent directory as PocketSphinx, so that the configure script
and project files can find it. On Windows, you will need to rename
'sphinxbase-X.Y' (where X.Y is the SphinxBase version number) to simply
'sphinxbase' for this to work.

To compile the SphinxTrain under MS Visual Studio 2010 (or newer - we test
with Visual C++ 2010 Express):

 1. load SphinxTrain.sln located in SphinxTrain directory
 2. compile all the projects in SphinxTrain (from SphinxTrain.sln)

MS Visual Studio will build the executables under .\bin\Release or
.\bin\Debug (depending on the version you choose on MS Visual Studio),
and the libraries under .\lib\Release or .\lib\Build.

If you are using cygwin, the installation procedure is very similar to
the Unix installation. 

Also, check the section title "All Platforms" above.

Once you finished with compilation, copy the pocketsphinx and sphinxbase
tools and dlls from sphinxbase\bin\Releae and pocketsphinx\bin\Release to
sphinxtrain\bin\Release folder. This will enable you to run the 
training process which expects to see all the tools and libraries in
sphinxtrain\bin\Release.

Acknowldegments
^^^^^^^^^^^^^^^

The development of this code has included support at different times
by various United States Government agencies, under different programs,
including the Defence Advanced Projects Agency (DARPA) and the
National Science Foundation (NSF). We are grateful for their support.

This work was built over a large number of years at CMU by most of the
people in the Sphinx Group. Some code goes back to 1986. The most
recent work in tidying this up for release includes the following,
listed alphabetically (at least these are the people who are most
likely able to help you).

Alan W Black (awb@cs.cmu.edu)
Arthur Chan (archan@cs.cmu.edu)
Evandro Gouvea (egouvea+@cs.cmu.edu)
Ricky Houghton (ricky.houghton@cs.cmu.edu)
David Huggins-Daines (dhuggins@cs.cmu.edu)
Kevin Lenzo (lenzo@cs.cmu.edu)
Ravi Mosur
Long Qin (lqin@cs.cmu.edu)
Rita Singh (rsingh+@cs.cmu.edu)
Eric Thayer

### Code checking

```
def updateMouth():
    lastMouthEvent = 0
    lastMouthEventTime = 0

    while( audio == None ):
        time.sleep( 0.1 )

    while isRunning:
        if( audio.mouthValue != lastMouthEvent ):
            lastMouthEvent = audio.mouthValue
            lastMouthEventTime = time.time()

            if( audio.mouthValue == 1 ):
                io.set( MOUTH_OPEN, 1 )
                io.set( MOUTH_CLOSE, 0 )
            else:
                io.set( MOUTH_OPEN, 0 )
                io.set( MOUTH_CLOSE, 1 )
        else:
            if( time.time() - lastMouthEventTime > 0.5 ):
                io.set( MOUTH_OPEN, 0 )
                io.set( MOUTH_CLOSE, 0 )
```

```
mouthThread = Thread(target=updateMouth)
mouthThread.start()
```