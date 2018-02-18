# `cmake` and `make` on W10
**NOTE**: The purpose of this repo is to help me learn cmake. This is NOT an exemplar template, but it might prove helpful to those wanting to get started with cmake on Windows 10!

Let's learn how to build a simple project on Windows 10 using `cmake` with the "Unix Makefiles" generator and `make`.

## Dependencies
- CMake
- GNU Make
- g++ compiler (mingw; I have it installed through Git For Windows)

This was originally written using cmake 3.10.2, make 3.81.4, and Git for Windows 2.16.1(4). Anything newer should work fine.

## Installing the tools
Git for Windows: https://git-scm.com/download/win
- Feel free to use any environment you want.
- I choose to use Git for Windows and the MinGW Installation Manager to install g++.

I've been using [Chocolatey](https://chocolatey.org/) as of late to install packages. The following commands require an elevated command prompt. Choose `Y[es]` when asked to run the installation scripts. I believe these tools also have Windows installers if you don't want to use Chocolatey.

`cinst cmake`

`cinst make`

## Project setup
Clone this repo into a location of choice.

`git clone [repo-url] [location]`

The file structure should look something like this:

```
.
|-- CMakeLists.txt
|-- README.md
|-- build
`-- src
    |-- CMakeLists.txt
    `-- main.cpp

2 directories, 4 files
```

- Add any source files to `./src`, and be sure to include them in the `add_executable` expression in `./src/CMakeLists.txt`.
- You can change the project name from "myprojectname" in `./CMakeLists.txt` and `./src/CMakeLists.txt`.

## Building
Navigate to the `./build` directory. This is where we will run `cmake` and `make`! Because I have the Visual Studio Build Tools installed (and it shows up first in the generators list), by default, my `cmake` uses the `Visual Studio 15 2017` generator. To see what generators are available on your machine, simply call `cmake` with the `help` argument.

```
$ cd ./build
$ cmake --help
...

Generators

The following generators are available on this platform:
  Visual Studio 15 2017 [arch] = Generates Visual Studio 2017 project files.
                                 Optional [arch] can be "Win64" or "ARM".
...

MSYS Makefiles               = Generates MSYS makefiles.
MinGW Makefiles              = Generates a make file for use with
                               mingw32-make.
Unix Makefiles               = Generates standard UNIX makefiles.

...
```

I want to generate a Makefile-based project, not a Visual Studio project. To choose a generator, we can pass the `G` argument along with the name of the generator.

```
$ cmake .. -G "Unix Makefiles"
-- The C compiler identification is GNU 6.3.0
-- The CXX compiler identification is GNU 6.3.0
-- Check for working C compiler: C:/MinGW/bin/gcc.exe
-- Check for working C compiler: C:/MinGW/bin/gcc.exe -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: C:/MinGW/bin/c++.exe
-- Check for working CXX compiler: C:/MinGW/bin/c++.exe -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/codebase/c++/cmake-template/build
```

Now, build the project using the GNU `make` command.

```
$ make
Scanning dependencies of target myprojectname
[ 50%] Building CXX object src/CMakeFiles/myprojectname.dir/main.cpp.obj
[100%] Linking CXX executable myprojectname.exe
[100%] Built target myprojectname
```

Success! The file structure now looks like this:

```
.
|-- CMakeLists.txt
|-- README.md
|-- build
|   |-- CMakeCache.txt
|   |-- CMakeFiles
|   |   `-- ...
|   |-- Makefile
|   |-- cmake_install.cmake
|   `-- src
|       |-- CMakeFiles
|       |   `-- ...
|       |-- Makefile
|       |-- cmake_install.cmake
|       `-- myprojectname.exe
`-- src
    |-- CMakeLists.txt
    `-- main.cpp

12 directories, 44 files
```

Notice how there is now an executable at `./build/src/myprojectname.exe`. Let's try running it.

```
$ pwd
/c/codebase/c++/cmake-template

$ ./build/src/myprojectname.exe
Hello, CMake!
```

That's it! I may expand this as I learn more and become familiar with these tools. Hopefully it helped!
