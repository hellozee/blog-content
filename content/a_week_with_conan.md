+++
title = "A Week with Conan"
date = 2019-09-30T20:00:28+05:30
tags = ["cpp", "conan", "package-manager", "languages"]
categories = ["language"]

+++

If someone has been following my posts, they would sure know, I write `C++` for most of the time, I spent to write any piece of code. The reaction to which most people resonate is, "ouch, you write c++, that must be really tough". To all of the people with this reaction, to be writing python is harder than `C++`. Okay, enough, lets come to today's topic, `conan`, a lot of times, I find people using the argument that, `C++` doesn't have any package manager like the other languages. Wrong, `C++` has a bunch of package managers, just no standard ones and `conan` is one of them. Last week, I took it for a test drive, since up to now, what I did was pulled in dependencies with the help of git submodules.

`conan` is developed using python, so it is available in PyPI. But the first thing I noticed, was that, they didn't have an IRC channel for queries, that is not something astonishing in this decade, but instead they had a Slack channel, which, to be fair, I don't understand. Other than I didn't find any real time chat for support, :hushed:. Ohh, `conan` being written in python saves a lot of hassle to install it, just a `pip3 install conan --user` will suffice.

The getting started page of the manual, listed an example of using poco library, easy to follow and replicate. And to be fair, I was remotely interested in reading the manual, I was more into getting a basic `Qt` project to work and increment the number of libraries one at a time.

Getting a basic Qt project was easy, also, the ability to use Python to write the configuration files, was a bonus. But as soon as I added GTest, the python configuration just, blew up. I had to resort the generic `txt` configuration format, for the fact that, it was not able to find the headers for GTest in the python configuration file, why, I don't know. But anyway, the best part was I could hook it up in my build system without any changes to CMake files. The configuration file looked liked this, 

```
[requires]                                                                      
qt/5.12.5@bincrafters/stable                                                    
gtest/1.8.1@bincrafters/stable                                                  
                                                                                
[generators]                                                                    
cmake                                                                           
                                                                                
[options]                                                                       
qt:shared=True                                                                  
```

And just a couple more lines, to the top level `CMakeLists.txt` file,

```cmake
 include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
 conan_basic_setup()
```

If I want to add more stuff then, I just do a `conan search <library name> --remote=<remote>` and add that under the `[requires]` section. I was told that `conan` had some problems with the KDE stuff, like platform specific plugins and all, but I am yet to try that, `:wq` for now, :slightly_smiling_face:.