# Getting Started

You have two options available
1) Get a working code base container using Docker, or 
2) Download the source code and its dependencies.

## Docker


For Multi-platform execution (Windows, MAC, Linux, Azure, AWS)

You can quickly get a contained working copy in few minutes of the
latest LAPKT version in the repository using Docker. For instructions,
please visit:

<https://hub.docker.com/r/lapkt/lapkt-public/>

## Download sources


The command:

```
    git clone https://github.com/LAPKT-dev/LAPKT-public.git <directory>
```
will create a clone of the LAPKT master repository in `<directory>`. The directory is created if it does not yet exist.

### Requirements


LAPKT requires the following libraries & tools:

-   scons
-   boost
-   boost::program\_options
-   varjudy

optional FF-parser:

-   makedepend
-   flex
-   bison

optional FD-Parser:

-   python
-   python-dev
-   boost::python-dev

In order to compile LAPKT, we recommend g++ 4.7 or better. However, any
compiler able to handle both boost libraries and C++11 standard new
features, should also be usable (we have been able to compile it under
Visual Studio 2010, llvm, and the new Linux bash shell on windows 10).
makedepend comes in xutils-dev package. 

### Building LAPKT


In order to build LAPKT you need to install scons (a GNU Makefile
replacement) in your system. Refer to <http://www.scons.org> for
directions on how to achieve this.

In order to compile some of the examples, you will also need a version
\>= 1.49 of the Boost C++ libraries available on your system. You can
check the version you have either manually by looking at the macro
defined in `boost/version.hpp` or, on debian systems, by running
`dpkg -s libboost-dev`. 

Finally, LAPKT requires the Judy library
(http://judy.sourceforge.net/index.html) to support the bitmap array
class 'Varset Judy'. NOTE: This dependency will be optional or entirely
deprecated in the future.

The following command installs all the dependencies on Ubuntu version \>
12.04LTS:


    sudo apt-get update && sudo apt-get install --no-install-recommends -y \
    build-essential \
    ca-certificates \
    xutils-dev \
    scons \
    gcc-multilib \
    flex \
    bison \
    python \
    python-dev \
    python3 \
    python3-dev \
    libboost-python-dev \
    libboost-dev \
    libjudy-dev \
    libboost-program-options-dev \
    g++-multilib

#### Build Instructions


Issue the command
```
scons
```
at the root of the source directory to obtain the (static) library
containing essential data structures and other miscellaneous utilities.
If debug symbols are needed, the command
```
scons debug=1
```
builds the library with optimizations disabled and debug symbols
enabled.

If you want to use FF-parser, compile the ff into a library by running
the following commands:

    cd external/libff
    make clean
    make depend
    make

If you are a Mac OS X user, run this command to create the final dynamic
library
```
libtool -o libff.a *.o
```
As Mac OS X don\'t like static libraries, if you run scons and you get
the following error:

    ld: library not found for -lcrt0.o

edit the SConstruct and comment (add \#) the following line:

    common_env.Append( LINKFLAGS = [ '-static' ] )

#### Compiling Examples and Planners

To compile any example go to a specific folder and type

     scons 

In FD-parser based examples type

     ./build.py 

The examples for the 'planner agnostic' interface can be found on

    examples/agnostic-examples

and cover the following topics:

    * agnostic-examples/assembling_strips_problems

        Shows how to define a STRIPS planning problem programatically.

    * agnostic-examples/successor_generation
        
        Discusses the different way of generating successors during search.

    * agnostic-examples/bfs
    * agnostic-examples/bfs-double-queue 
    * agnostic-examples/bfs-double-queue-secondary-heuristic

        Shows how can one assemble available components to deliver a
        planner built around a BFS search engine, with multiple queues and
        secondary heuristics, on a parametrized planning task.

    * agnostic-examples/das

        Shows how can one assemble available components to deliver a
        planner built around Deadline Aware Search.

Alternatively, To learn how to ensemble different heuristics go through
simple planners like

    planners/generic-best_first-ffparser

To learn how to use or create a planner using FD-parser, copy and edit a
simple planner like

    planners/siw

and to learn how to use or create a planner using FF-parser

    examples/ff-interface

or copy and edit a simple Breadth first search planner like

    examples/agnostic-examples/brfs

or start from the classic heuristic Search Planner

    examples/agnostic-examples/bfs-hmax

        Shows how to assemble a best-first search using h_max with multiple modes: greedy/delayed/anytime,
        over a task specified in PDDL and parsed by FF-parser
