# TechnicalReview.pdf

## eotk deployment for www.example.com

## AppEngine deployment with Django and local SQL database in container for www.example.com

## Netflix implementation (client and server) with Twisted

## Home corporate security measures

## Compiling Tensorflow with no AVX support
I had to compile TensorFlow. At the time, I totally forgot about just simply using Python wheels,
and indeed the reminder of it made it totally unnecessary to compile, but it’s still worth noting the
compilation process (before it was abandadend). I’m saying that the insructions at
https://www.tensorflow.org/install didn’t work for me because of my machine.

Of course I’m sure we all can agree: don’t try looking at ANY content in the
github.com/tensorflow/tensorflow directory. You only want to USE TensorFlow: you don’t want to
understand it, or deal with it. So only do the work required to generate the wheel file that you
need.

So your goal is to get that Python Wheel file. I’ve found sources of them online thankfully, but I
still have a space computer compiling TensorFlow just to see if I can get the best bin ary I can (the
ones online use prior versions of TF).

It takes like a full 24 hours to compile TensorFlow. Sometimes the computer would freeze after 12
hours and you have to start it again, making sure that that doesn’t happen again the next time. I
figured out the specific flags needed, and found 3 possible places to place them: ./configure
inputs, the bazel command line, and a .tf_bazelrc resource file. One thing that puts your mind at
ease is that the time it takes to compile TensorFlow is nothing compared to the training time you’ll
be doing anyway (lol). In other words, how long it takes to compile TensorFlow pales in
comparison to how long it will take for TensorFlow to train on your data anyway, after you’re done
compiling TensorFlow.

- I got to understand the TensorFlow developer Docker image. Pretty nifty, and I can easily
see how it can be industrialized in a cloud environment to of course build almost any
combination of Python version and TensorFlow version, with or without AVX (or whatever
compile-time option concerns you at the time). Too much work though – just get the wheel
and get out.

- I eventually remembered that you can find already-compiled wheels on GitHub, and I did
find one that worked, but it’s for an older version of TensorFlow (2.5.1), and 2.8 is out right
now, and so a TF 2.8 wheel with no AVX might be worth the wait.

- Just the target that just builds the pip package has like 27,000 build targets. That’s tens of
thousands of text files of source code. Can you imagine dealing with thirty-thousand files in
a folder? This codebase is like the source code to the operating system of that robot from
Metal Gear Solid.

- Sloccount is a computer program that simply counts how many lines of code there are in a
folder full of source code. It most always returns in less than a second. I ran that program
on the TensorFlow codebase, it took my machine at least 4 minutes. There’s over 2 million
lines of code. For example, there’s these 2 files tfl_ops.cc and legalize_tf.cc that each have
3700 and 2300 lines of code; it took 3+ hours to compile just those 2 files.

## Recent technical problems being worked on

Here are some recent technical problems or projects being worked on, that may or may not warrant a seperate repository for, but none-the-less should be described somewhere:

- [Boost MPI example, using only Docker](boost_mpi_example.md)
- [Docker compose](DockerCompose.md)
- [EOTK and Datalab container review](eotk_datalab.md)
- [A random Arduino kit to play with](arduino.md)
- [Deployment on www.PythonAnywhere.com](python_anywhere.md)
- [Urgent shutdown of cloud resources](cloud_shutdown.md)
- [Failed laptop encrypted hard drive](failed_hard_drive.md)
- [Open court system project](court_system.md)
- [Android development](android.md)
