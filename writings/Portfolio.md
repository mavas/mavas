# Portfolio.pdf (as of January 2023)

## Introduction

This document is entirely made for employment purposes.

Each section (aside from this one) describes a technical problem that was worked on; in no particular order.

<!--
## Git usage

I use Git all the time.  Along with Git Flow.  I used to use SVN, and even Bazaar.  My focus is on the `main` branch, updating the `README.md` file with the latest release notes, creating `git tag`s on that branch, and then quickly throwing those `feature/miscellaneous` branches away.  I have the original Git Flow picture printed out and posted on my wall next to the computer.

- https://nvie.com/posts/a-successful-git-branching-model/
-->

## Production deployment: MeleeSearch REST API endpoint (over Tor network)

So the results of my research into Super Smash Bros. Melee video game footage yielded a few model files which can be used to automatically analyize data, and you can expose that data through an application programming interface (API) accessible over the network using the REST protocol.

Django Rest Framework is used, deployed as a running Docker container, and it's accessible over the Tor network as a Tor Onion Service.

## Tensorflow work, data engineering, data curation

All data problems revolve around your particular collection of data, and at the forefront of that is a proprietary web application I developed for the curation of video data regarding the video game called "Super Smash Bros. Melee".  At the core is Django, which is essentially 2 things: an entirely web-based interface to whatever you're doing, and heavy use of an associated PostgreSQL database.  This all then interfaces with a variety of Python libraries: models, datasets, cloud, youtube-dl, django-extensions, whoosh.

## Task: Failed laptop encrypted hard drive

_Linux Unified Key Setup, learning its commands, reading its source code, and running `dd`._

I came home to find that my primary laptop's hard drive failed, and I had to just deal with it.  I had to learn and deal with the LUKS Linux encryption file system thing, not only having to discover/learn/run new commands (like `cryptsetup`, and `luksOpen`), but dealing with the source code itself **of** those command line tools.  All of the data was valuable, so I had to be careful, and so I had to know exactly what was going on, so dealing with these commands, and  their source code, was important to proceed with; thankfully the code was rather short.  I had to run the `dd if=/dev/sda of=/dev/sdb` command in attempts to at least perfectly mirror/backup the data, so that you can simply install Ubuntu back on it and the hard drive will be good as new, but I ran in to some errors with that command, and so now I'm stuck, and the laptop is just sitting here.  In the meantime it was fastest though to just use my older laptop for job hunting, and then get a job, and then get back to the issue.

Anyway, I usually use Ubuntu, and sometimes its using some transperant encryption thing underneath as the file system, and the point is that it really is a transperant thing, meaning you're not supposed to really need to think about it.  But with this issue, it suddenly became **the** issue and one then has to dig under the hood and discover and learn about and deal with yet another new layer of software *stuff*.

## Production deployment: a Mastodon instance

When news about Mastodon came out, I of course didn't want to **use** it all, but instead **launch my own instance**.

But why?  What would you call it?  And what's it's purpose?  Well, I'm learning a knew spoken language, and so maybe it should be about that language.  That language community doesn't particularly at all have a presence in the Mastodon network, and so it looked like a great opportunity to be at the forefront of something, and create a new instance and likely obtain a large number of users reliably.

And it's here!  Download your favorite Mastodon client and visit `mastodon.jbo` to see the latest of my work.

The setup is all quite simple, thanks to Docker.  There's a `docker-compose.yml` file in the top directory, and there is of course upstream-provided instructions for deploying, administering, and maintaining an instance, and I of course read all of it.

- https://github.com/anon5r/mastodon-documentation/blob/master/Running-Mastodon/Docker-Guide.md.  One of the funniest things is that other people's documentation is better than the official documentation, like this repository.  Anyway, thankfully Docker and translation are first-class support.

## Contributing spoken language translations for upstream Mastodon

The section just above this one speaks about setting up a production server, but I can of course contribute some code changes to the upstream server itself.  Namely, in the form of language translations.

Most huge open source projects have translations involved, such that folks can contribute language translations for their favorite language.  There weren't any translations for the purpose of my particular Mastodon instance, and so this was a great opportunity (for me) too.

See my fork of the official Mastodon repository for my translations so far: https://github.com/mavas/mastodon.

- https://github.com/anon5r/mastodon-documentation/blob/master/Contributing-to-Mastodon/Translating.md

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

You want to make frequent releases to production.  There is a Django project, in a single folder that was created with `django-admin startproject example`, and this folder is a Git repository started with `git init .`, and releases are `git tag`ed on it.  Each time you make a release in this folder, you do `gcloud app deploy`, and after that command finishes running (it takes at most 2 minutes), the new site is deployed to your www.example.com domain.

This is by far the easiest deployment I've ever done, but it's very effective.

However, to save costs, it's possible to use your own SQL database that is running locally on your computer in a Docker container.. instead of using a costly Cloud SQL instance.  You your Django `settings.py` file, you can plug in your IP address, and make sure to login to your modem/router and open up the ports to allow access, and it works perfectly.  You have to take extra security measures, but so long as that is in place, you save money doing it this way (Cloud SQL is suprisingly expensive actually, running a few hundred dollars per month).

## Production deployment and implementation: Netflix clone (client and server) via Twisted

> You can implement something similar to Netflix or Disney+.

There's a server program, and many client programs that connect to it; none of the clients know about each other or even interact with each other, unlike a video game.  The server has all of the content, and the clients simply request content to be streamed to it, and the server handles it all.

The fancy/complicated stuff happens in the server; the client is just a nice UI that streams content to the user who is viewing it.  Contrastingly, if you have lots of movies at home, and you wish to watch them, you'd have to use some local software like Windows Media Player, or the VLC media player, for playback.  That's not how Netflix works: the Netflix app that everyone uses simply streams content from remote servers.

## Task: Compiling Tensorflow, with no AVX support

I once had to compile TensorFlow.  While I eventually found out that I didn't actually need to compile it (you can instead hopefully find a working Wheel file somewhere), this section documents my efforts at compiling that codebase.

The insructions at https://www.tensorflow.org/install didn’t work for me on any of my machines.  Everything appeared to have been installed correctly, but when I started up the Python interpreter and tried to do `import tensorflow as tf`, I got an error which mentioned the word `AVX` in it, and then the interpreter segfaulted.  Investigation revealed that it had something to do with the CPU architecture being used, combined with the Python wheel binary that was installed and being used.  It turns out that the `pip` installation mechanism isn't smart enough to decide not to install something while considering CPU architecture.  Part of solving the problem involved 1.) my already-present familiarity with the Gentoo operating system, and 2.) seeing this page: https://packages.gentoo.org/packages/sci-libs/tensorflow.  That page confirms that `avx`/`avx2` is a Gentoo `USE` flag that can be turned on and off; so TF needs to be compiled __without__ AVX support, and, for some reason, the Python wheel installed on my system requires AVX.

Of course I’m sure we all can agree: don’t try looking at ANY content in the [github.com/tensorflow/tensorflow](https://github.com/tensorflow/tensorflow/tree/master/tensorflow) directory. You only want to _USE_ TensorFlow: you don’t want to _understand_ it, or _deal_ with it (installation issues, etc.). So only do the work required to generate the wheel file that you need.

So your goal is to get that Python Wheel file. I’ve found sources of them online thankfully, but I still have a spare computer compiling TensorFlow just to see if I can get the best binary I can (the ones online use outdated versions of TF).

It takes like a full 24 hours to compile TensorFlow. Sometimes the computer would freeze after 12 hours and you have to start it again, making sure that that doesn’t happen again the next time. I figured out the specific flags needed, and found 3 possible places to place them: `./configure` inputs, the `bazel` command line, and a `.tf_bazelrc` resource file. One thing that puts your mind at ease is that the time it takes to compile TensorFlow is nothing compared to the training time you’ll be doing anyway (lol). In other words, how long it takes to compile TensorFlow pales in comparison to how long it will take for TensorFlow to train on your data anyway, after you’re done compiling TensorFlow.

- I got to understand [the TensorFlow developer Docker image](https://www.tensorflow.org/install/source#docker_linux_builds). Pretty nifty, and I can easily see how it can be industrialized in a cloud environment to of course build almost any combination of Python version and TensorFlow version, with or without AVX (or whatever compile-time option concerns you at the time). Too much work though and not necessary, ever since I learned/remembered that you just need a pre-compiled and compatible Python wheel file somewhere, and plenty of them are on GitHub from contributors working on the same thing I was tasked with – just get the wheel and get out.

- I eventually remembered that you can find already-compiled wheels on GitHub, and I did
find one that worked, but it’s for an older version of TensorFlow (2.5.1), and 2.8 is out right
now, and so a TF 2.8 wheel with no AVX might be worth the wait.

- Just the target that just builds the pip package has like 27,000 build targets. That’s tens of
thousands of text files of source code. Can you imagine dealing with thirty-thousand files in
a folder? This codebase is like the source code to the operating system of that robot from
Metal Gear Solid.

- `Sloccount` is a computer program that simply counts how many lines of code there are in a
folder full of source code.  It most always returns in less than a second.  I ran that program
on the TensorFlow codebase, and it took my machine at least 4 minutes. There’s over 2 million
lines of code. For example, there’s these 2 files [tfl_ops.cc](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/compiler/mlir/lite/ir/tfl_ops.cc) and [legalize_tf.cc](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/compiler/mlir/tosa/transforms/legalize_tf.cc) that each have 4,000 and 2300 lines of code; it took 3+ hours to compile just those 2 files.

- It turns out that there's a whole community of people that take the time and expertise to compile Tensorflow wheels and redistribute them, precisely b/c it's a common problem.  See [this](https://github.com/davidenunes/tensorflow-wheels) and [this](https://www.eggwall.com/2020/09/compiling-tensorflow-without-avx.html).

<!--
## NodeJS experience

Most of my experience using this software is with:
 
- Modification and understanding the `DataLab` project source code, and
- Deployment of a Mastodon instance

Both of these projects make use of Docker and incorporate a running `Node` server as a core component of its operation.  My involvment regarding the DataLab project is its role in performance regarding data processing, and its involvement regarding Mastodon is its role in streaming social media and video content in an efficient manner to many client program processes.
--->

## Things I've done with C/C++

- I first started out with C++, and then much later learned Python.  Some say you get a different kind of engineer from the one that learns Python first and then has to learn C.  I understood the call stack, walked through things slowly with the **gdb** tool, made a game loop with it, etc.  The first compiler that I found that worked decent was Borland C++, which is still around today.  I used to lookup www.cplusplus.com **constantly**, and that web site is still up and looks the same.  C++ allows for very under-the-hood understanding of exactly how things are performed by the machine/computer, whereas Python is designed to hide these types of things.. automatic garbage collection for example (versus manually freeing memory).  Once you have a good grasp of the syntax for argument-passing (call by reference or call by value?), then you never mess it up again and you can focus.

- **Olimar's Escape** is a text-based RPG game I made.  It features a game loop - of course - and is incomplete, but taught me that things can get big really quickly.  I had to start coming up with characters, and stories, and scenes, and speech, and items that need to go in the rooms, and all kinds of things.  It takes a lot to make a full video game.  The code is [here](https://github.com/mavas/Olimar-Escape).  The important thing about this though - in regards to my current expertise with C++ - is that I was thinking _entirely_ at a high level while programming this using only C++; in other words, I was thinking about _a whole game_, in standard C++.  No other libraries were used, so it's just using raw C++ (variables, functions, classes, reading from files, etc.), to make a text-based RPG game; it didn't even use the standard template library (STL).

- I kind of got into the Boost libraries but didn't stay around for too long, it turns out.  Boost.Python was used during an internship to make C++ bindings between C++ and Python.  There were numerous other options at the time but we settled on Boost.  The project ended up not using my work and using some other language binding tool.  OpenCog uses Boost extensively and successfully, and I have had to deal with that codebase before.

- I once found the [DexDrive](https://github.com/fbriere/linux-dexdrive) Linux C code on the THIRD page of a Google search, and then downloaded it compiled it and ran it, in order to save songs I had made on a video game for a Playstation memory card.  It's a non-standard device, that you feed your memory cards into, and it can transfer the data to your computer for backup purposes.  The device surely works for Windows, but I had to find the code online for Linux, and it was in some random person's repository.  This is one of those classic examples of hardware and/or software written for Windows, but you can still find an open source Linux driver somewhere and it works great and is better than the Windows software that never gets updated.

- **Compiling OpenCV for the Python language bindings**.  It's always best to manually go to the opencv.org web site and download and extract the source code and compile it yourself using the CMake tool.  Practically the only reason to need to deal with compiling OpenCV's source code is when you want access to the Python language bindings.  For this, you have to add certain flags to your `cmake -DCMAKE_BUILD_TYPE=Debug ..` command, and then you find the **cv2.so** file in there somewhere \[you understand of course that it is this **cv2.so** file that's entirely responsible for why `import cv2` works in your Python script\].

- I once had to work a full-time job doing C++ investigative development for a data operation.  I had to create a custom binary which moved data from place to another, likely with Apache Flume or similar.  This was in the last 5 years, and is my most recent and professional C++ experience.

- All too often, you're on the web and you download some code and you have to compile it and deal with it, and this code is in C or C++, and you have to actually mess (edit the code and recompile) with it.  Often times is a small amount of code, like the kind that would interface with a toaster.  Take [Packet Storm Security](https://www.packetstormsecurity.com/).

- Firmware is pretty important.  chipsec is a cool tool.  I heard lately that GoLang is popular with malware authors; I don't know the language yet.  ThinkPwn is a nasty exploit that deals with the UEFI stuff, that I've been reading about lately.
- **C++'s relationship to C**.  I think I prefer C, because maybe that templating stuff isn't too necessary, but some libraries make heavy use of dlib and Boost. I had a copy of the classic K&R book.

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
