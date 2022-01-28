# Things I've done with C++

- I first started out with C++, and much later learned Python.  Some say you get a different kind of engineer from the one that learns Python first and then has to learn C.  I understood the call stack, walked through things slowly with the **gdb** tool, made a game loop with it, etc.  The first compiler that I found that worked decent was Borland C++, which is still around today.  I used to lookup www.cplusplus.com **constantly**, and that web site is still up and looks the same.

- Olimar's Escape.  My first text-based RPG game.  It features a game loop - of course - and is incomplete, but taught me that things can get big really quickly.

- I kind of got into the Boost libraries but didn't stay around for too long, it turns out.  I did Google's Summer of Code and used Boost.Python to make C++ bindings between C++ and Python.  There were numerous other options at the time but we settled on Boost.  The project ended up not using my work and using some other language binding tool.  OpenCog uses Boost extensively and successfully, and I have had to deal with that codebase before.

- I once found the [DexDrive](https://github.com/fbriere/linux-dexdrive) Linux C code on the THIRD page of a Google search, and then downloaded it compiled it and ran it, in order to save songs I had made on a video game for a Playstation memory card.  It's a non-standard device, that you feed your memory cards into, and it can transfer the data to your computer for backup purposes.  The device surely works for Windows, but I had to find the code online for Linux, and it was in some random person's repository.

- Compiling OpenCV for the Python language bindings.  It's always best to manually go to the opencv.org web site and download and extract the source code and compile it yourself using the CMake tool.  Practically the only reason to need to deal with compiling OpenCV's source code is when you want access to the Python language bindings.  For this, you have to add certain flags to your "cmake -DCMAKE_BUILD_TYPE=Debug .." command, and then you find the **cv2.so** file in there somewhere.  CMake is pretty nice in that it's much easier to deal with than Makefiles; CMake _generates_ Makefiles.

- I once had to work a full-time job doing C++ investigative development for a data operation.  I had to create a custom binary which moved data from place to another, likely with Apache Flume or similar.

- All too often, you're on the web and you download some code and you have to compile it and deal with it, and this code is in C or C++, and you have to actually mess (edit the code and recompile) with it.  Often times is a small amount of code, like the kind that would interface with a toaster.  Take [Packet Storm Security](https://www.packetstormsecurity.com/).

- Firmware is pretty important.  chipsec is a cool tool.  I heard lately that GoLang is popular with malware authors; I don't know the language yet.
