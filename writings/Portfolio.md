# Portfolio.pdf (as of January 2023)

## Tensorflow work, data engineering, data curation

All data problems revolve around your particular collection of data, and at the forefront of that is a proprietary web application I developed for the curation of video data regarding the video game called "Super Smash Bros. Melee".  At the core is Django, which is essentially 2 things: an entirely web-based interface to whatever you're doing, and heavy use of an associated PostgreSQL database.  This all then interfaces with a variety of Python libraries: models, datasets, cloud, youtube-dl, django-extensions, whoosh.

## Failed laptop encrypted hard drive

_Linux Unified Key Setup, reading its source code, learning its commands, and running 'dd'_

I came home to find that my primary laptop's hard drive failed, and I had to just deal with it.  I had to learn and deal with the LUKS Linux encryption file system thing, not only having to discover/learn/run new commands (like `cryptsetup`, and `luksOpen`), but dealing with the source code itself **of** those command line tools.  All of the data was valuable, so I had to be careful, and so I had to know exactly what was going on, so dealing with these commands, and  their source code, was important to proceed with; thankfully the code was rather short.  I had to run the `dd if=/dev/sda of=/dev/sdb` command in attempts to at least perfectly mirror/backup the data, so that you can simply install Ubuntu back on it and the hard drive will be good as new, but I ran in to some errors with that command, and so now I'm stuck, and the laptop is just sitting here.  In the meantime it was fastest though to just use my older laptop for job hunting, and then get a job, and then get back to the issue.  Anyway, I usually use Ubuntu, and sometimes its using some transperant encryption thing underneath as the file system, and the point is is that it really is a transperant thing, meaning you're not supposed to really need to think about it.  But with this issue, it suddenly became **the** issue and one then has to dig under the hood and discover and learn about and deal with yet another new layer of software *stuff*.

## Translating Mastodon, deploying an instance

When news about Mastodon came out, I of course didn't want to **use** it all, but instead **launch my own instance**.  But why?  What would you call it?  And what's it's purpose?  I'm learning a knew language, and so maybe it should be about that.  Oh and you can also contribute official translations into the software.

- https://github.com/anon5r/mastodon-documentation/blob/master/Contributing-to-Mastodon/Translating.md
- https://github.com/anon5r/mastodon-documentation/blob/master/Running-Mastodon/Docker-Guide.md.  One of the funniest things is that other people's documentation is better than the official documentation, like this repository.  Anyway, thankfully Docker and translation are first-class support.
- https://github.com/mavas/mastodon

## Production deployment: Web site as a Tor Onion Service

I recently had to develop and deploy a web site for a business guy.  He basically wanted a web forum, but didn’t know or want to know how to set one up, and he didn't want to maintain it, and he said he’s heard about “Tor” before and said that he’s sure that he wanted to use that.  I of course already knew exactly what he was talking about, and did it all for him.

It had to be deployed as a web site over the Tor network, and it needed to be up most of the time.  Docker compose was employed b/c of the multiple components involved: a PostgreSQL database, the web site itself, and a Tor service running constantly.  Django was used, along with https://github.com/ellmetha/django-machina; a fork was created to remove the dependency on Haystack, so that it instead just used Whoosh.  And those are all the components.

- https://github.com/dustyfresh/OnionIRC.  This repository has the minimal setup, which involves only one container, with an Ubuntu base image, the `supervisord` service which will be responsible for 2 services, which are an IRC server (NIRCD) and Tor itself.  It even includes minimal config files for all 3.  Of course it needed to be modified to serve a web site instead of an IRC server.
- https://community.torproject.org/onion-services/setup/
- https://community.torproject.org/onion-services/advanced/https/

A major consideration is that **you really want to be using the latest version of Tor**, and that means **you don't want to use the version that's packaged with Ubuntu**, and so Docker's [multi-stage builds](https://docs.docker.com/build/building/multi-stage/) are appropriate, where you use the first stage to build and compile the latest source code release of Tor into an executable, and then use that artifact in the next build stage.

## Production deployment: `eotk` Tor proxy for www.example.com web site

The section just above this one deals with the most-common scenario of "offering a computer service over the Tor network", but https://github.com/alecmuffett/eotk is used to create a sort of Tor proxy, which automatically creates the service from an already-existing web site.  `eotk` is used by Facebook, Washington Post, and various political groups to automatically offer their web site over the Tor network.

I did this for my own web site.  The Onion address will be posted here later.

<!--
## REST API development experience, and deployments

One custom project involves `Django REST Framework` regarding an authentication server.  It's significant in that it's intent is to be totally _unified_, across many other different deployments; namely, www.example.com and a mobile phone application released publicly in the Apple App store.

The 2 core functional components is exactly 2 third-party Django applications: `django-allauth` and `restframework'.  `allauth` performs practically all of the logical work, and `restframework` makes it all accessable with an API.
-->

## Production deployment: AppEngine, Django, domain registration, and local container SQL database (for www.example.com)

A good and easy production-grade deployment to an official `www.example.com` web domain is described here.  All you need is a cloud account, a Django project, and.. that's it.

## Production deployment and implementation: Netflix clone (client and server) via Twisted

You can implement something similar to Netflix or Disney+.  There's a server program, and many client programs that connect to it; none of the clients know about each other or even interact with each other, unlike a video game.  The server has all of the content, and the clients simply request content to be streamed to it, and the server handles it all.

The fancy/complicated stuff happens in the server; the client is just a nice UI that streams content to the user who is viewing it.  Contrastingly, if you have lots of movies at home, and you wish to watch them, you'd have to use some local software like Windows Media Player, or the VLC media player, for playback.  That's not how Netflix works: the Netflix app that everyone uses simply streams content from remote servers.

## Compiling Tensorflow, with no AVX support

I once had to compile TensorFlow.  While I eventually found out that I didn't actually need to compile it (you can instead hopefully find a working Wheel file somewhere), this section documents my efforts at compiling that codebase.

The insructions at https://www.tensorflow.org/install didn’t work for me on any of my machines.  Everything appeared to have been installed correctly, but when I started up the Python interpreter and tried to do `import tensorflow as tf`, I got an error which mentioned the word `AVX` in it, and then the interpreter segfaulted.  Investigation revealed that it had something to do with the CPU architecture being used, combined with the Python wheel binary that was installed and being used.  It turns out that the `pip` installation mechanism isn't smart enough to decide not to install something while considering CPU architecture.  Part of solving the problem involved 1.) my already-present familiarity with the Gentoo operating system, and 2.) seeing this page: https://packages.gentoo.org/packages/sci-libs/tensorflow.  That page confirms that `avx`/`avx2` is a Gentoo `USE` flag that can be turned on and off; so TF needs to be compiled __without__ AVX support, and, for some reason, the Python wheel installed on my system requires AVX.

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

- It turns out that there's a whole community of people that take the time and expertise to compile Tensorflow wheels and redistribute them, precisely b/c it's a common problem.  See [this](https://github.com/davidenunes/tensorflow-wheels) for example.

<!--
## NodeJS experience

Most of my experience using this software is with:
 
- Modification and understanding the `DataLab` project source code, and
- Deployment of a Mastodon instance

Both of these projects make use of Docker and incorporate a running `Node` server as a core component of its operation.  My involvment regarding the DataLab project is its role in performance regarding data processing, and its involvement regarding Mastodon is its role in streaming social media and video content in an efficient manner to many client program processes.
--->

## Recent technical problems being worked on

Here are some recent technical problems or projects being worked on, that may or may not warrant a seperate repository for, but none-the-less should be described somewhere:

- [Boost MPI example, using only Docker](boost_mpi_example.md)
- [Docker compose](DockerCompose.md)
- [EOTK and Datalab container review](eotk_datalab.md)
- [A random Arduino kit to play with](arduino.md)
- [Deployment on www.PythonAnywhere.com](python_anywhere.md)
- [Urgent shutdown of cloud resources](cloud_shutdown.md)
- [Open court system project](court_system.md)
- [Android development](android.md)
