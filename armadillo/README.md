### Armadillo: C++ Library for Linear Algebra & Scientific Computing  
http://arma.sourceforge.net

Copyright 2008-2020 Conrad Sanderson (http://conradsanderson.id.au)  
Copyright 2008-2016 National ICT Australia (NICTA)  
Copyright 2017-2020 Arroyo Consortium  
Copyright 2017-2020 Data61, CSIRO  

---

### Quick Links  

- [download latest stable release](http://arma.sourceforge.net/download.html)
- [documentation for functions and classes](http://arma.sourceforge.net/docs.html)
- [bug reports & questions](http://arma.sourceforge.net/faq.html)  

---
 
### Contents

1.  [Introduction](#1-introduction)
2.  [Citation Details](#2-citation-details)
3.  [Distribution License](#3-distribution-license)

4.  [Compilers and External Dependencies](#4-compilers-and-external-dependencies)

5.  [Linux and macOS: Installation](#5-linux-and-macos-installation)
6.  [Linux and macOS: Compiling and Linking](#6-linux-and-macos-compiling-and-linking)

7.  [Windows: Installation](#7-windows-installation)
8.  [Windows: Compiling and Linking](#8-windows-compiling-and-linking)

9.  [Support for OpenBLAS and Intel MKL](#9-support-for-openblas-and-intel-mkl)
10. [Support for ATLAS](#10-support-for-atlas)
11. [Support for C++11 / C++14 Features](#11-support-for-c11-c14-features)
12. [Support for OpenMP](#12-support-for-openmp)

13. [Documentation](#13-documentation)
14. [API Stability and Versioning](#14-api-stability-and-versioning)
15. [Bug Reports and Frequently Asked Questions](#15-bug-reports-and-frequently-asked-questions)

16. [MEX Interface to Octave/Matlab](#16-mex-interface-to-octavematlab)
17. [Related Software Using Armadillo](#17-related-software-using-armadillo)

---

### 1. Introduction

Armadillo is a high quality C++ library for linear algebra and scientific computing,
aiming towards a good balance between speed and ease of use.

It's useful for algorithm development directly in C++,
and/or quick conversion of research code into production environments.
It has high-level syntax and functionality which is deliberately similar to Matlab.

The library provides efficient classes for vectors, matrices and cubes,
as well as 200+ associated functions covering essential and advanced functionality
for data processing and manipulation of matrices.

Various matrix decompositions are provided through integration with LAPACK,
or one of its high performance drop-in replacements
(eg. OpenBLAS, Intel MKL, Apple Accelerate framework, etc).

A sophisticated expression evaluator (via C++ template meta-programming)
automatically combines several operations (at compile time) to increase speed
and efficiency.

The library can be used for machine learning, pattern recognition, computer vision,
signal processing, bioinformatics, statistics, finance, etc.

Authors:
  * Conrad Sanderson - http://conradsanderson.id.au
  * Ryan Curtin      - http://ratml.org

---

### 2: Citation Details

Please cite the following papers if you use Armadillo in your research and/or software.  
Citations are useful for the continued development and maintenance of the library.

  * Conrad Sanderson and Ryan Curtin.  
    Armadillo: a template-based C++ library for linear algebra.  
    Journal of Open Source Software, Vol. 1, pp. 26, 2016.  
  
  * Conrad Sanderson and Ryan Curtin.  
    A User-Friendly Hybrid Sparse Matrix Class in C++.  
    Lecture Notes in Computer Science (LNCS), Vol. 10931, pp. 422-430, 2018.

---

### 3: Distribution License

Armadillo can be used in both open-source and proprietary (closed-source) software.

Armadillo is licensed under the Apache License, Version 2.0 (the "License").
A copy of the License is included in the "LICENSE.txt" file.

Any software that incorporates or distributes Armadillo in source or binary form
must include, in the documentation and/or other materials provided with the software,
a readable copy of the attribution notices present in the "NOTICE.txt" file.
See the License for details. The contents of the "NOTICE.txt" file are for
informational purposes only and do not modify the License.

---

### 4: Compilers and External Dependencies

Armadillo makes extensive use of template meta-programming and many other
advanced C++ features.  As such, C++ compilers which do not fully implement
the C++ standard may not work correctly.

The functionality of Armadillo is partly dependent on other libraries:
LAPACK, BLAS (preferably OpenBLAS), ARPACK and SuperLU.
LAPACK and BLAS are used for dense matrices,
while ARPACK and SuperLU are used for sparse matrices.

Armadillo can work without the above libraries, but its functionality will be reduced.
Basic functionality will be available (eg. matrix addition and multiplication),
but operations like eigen decomposition or matrix inversion will not be.
Matrix multiplication (mainly for big matrices) may not be as fast.

As Armadillo is a template library, we recommended that optimisation
is enabled during compilation of programs that use Armadillo.
For example, for GCC and Clang compilers use -O2 or -O3

---

### 5: Linux and macOS: Installation

* Step 1:
  Ensure a C++ compiler is installed on your system.

   - On macOS systems you will need to install Xcode (version 8 or later)
     and then type the following command in a terminal window:  
     xcode-select --install

* Step 2:
  Ensure the CMake tool is installed on your system.
  You can download it from http://www.cmake.org
  or (preferably) install it using your package manager.

  - On Linux-based systems, you can get CMake using dnf, yum, apt, aptitude, ...
  - On macOS systems, you can get CMake through MacPorts or Homebrew.

* Step 3:
  Ensure LAPACK and BLAS (or preferably OpenBLAS) are installed on your system.
  On macOS this is not necessary.

  - For better performance, we recommend installing the OpenBLAS library.
    See http://www.openblas.net/  

  - If you are using sparse matrices, also install ARPACK and SuperLU.
    Caveat: only SuperLU version 5.2 can be used!

  - On Linux-based systems, the following libraries are recommended
    to be present: OpenBLAS, LAPACK, SuperLU and ARPACK.
    It is also necessary to install the corresponding development
    files for each library. For example, when installing the "lapack"
    package, also install the "lapack-devel" or "lapack-dev" package.
  
* Step 4:
  Open a terminal window, change into the directory that was created
  by unpacking the armadillo archive, and type the following command:

    cmake .

  - The full stop separated from "cmake" by a space is important.

  - CMake will detect which relevant libraries are installed on your system
    (eg. OpenBLAS, LAPACK, SuperLU, ARPACK, etc)
    and will modify Armadillo's configuration correspondingly.
    CMake will also generate the Armadillo run-time library,
    which is a wrapper for all the detected libraries.

  - By default, cmake assumes that the Armadillo library and the
    corresponding header files are going to be installed in the default 
    system directory (eg. in the /usr hierarchy in Linux-based systems).
    If you wish to install the library and headers in an alternative directory,
    use the additional option CMAKE_INSTALL_PREFIX in this form:

    cmake . -DCMAKE_INSTALL_PREFIX:PATH=alternative_directory

  - If you need to re-run cmake, it's a good idea to first delete the
    "CMakeCache.txt" file (not "CMakeLists.txt").

  - Caveat: out-of-tree builds are currently not fully supported;
     eg, creating a sub-directory called "build" and running cmake ..
     from within "build" is currently not supported.

  - Caveat: if you are installing Armadillo in a non-system directory,
    make sure your C++ compiler is configured to use the "lib" and "include"
    sub-directories present within this directory.  Note that the "lib"
    directory might be named differently on your system.
    On recent 64 bit Debian & Ubuntu systems it is "lib/x86_64-linux-gnu".
    On recent 64 bit Fedora & RHEL systems it is "lib64".

* Step 5:
  To generate the run-time armadillo library, type the following command:

    make

* Step 6:
  If you and have access to root/administrator/superuser privileges
  (ie. able to use "sudo") and didn't use the CMAKE_INSTALL_PREFIX option,
  type the following command:

    sudo make install

  If you don't have root/administrator/superuser privileges,
  make sure that you use the CMAKE_INSTALL_PREFIX option in Step 4,
  and type the following command:

    make install

---

### 6: Linux and macOS: Compiling and Linking

The "examples" directory contains several quick example programs
that use the Armadillo library.

In general, programs which use Armadillo are compiled along these lines:

    g++ example1.cpp -o example1 -O2 -larmadillo

If you want to use Armadillo without installation
(ie. without the runtime library generated by CMake during installation),
compile along these lines:

    g++ example1.cpp -o example1 -O2 -I /home/blah/armadillo-7.200.3/include -DARMA_DONT_USE_WRAPPER -lblas -llapack

The above command line assumes that you have unpacked the armadillo archive into /home/blah/  
You will need to adjust this for later versions of Armadillo (ie. change the 7.200.3 part)
and/or if you have unpacked the armadillo archive into a different directory.

Replace -lblas with -lopenblas if you have OpenBLAS.
On macOS, replace -lblas -llapack with -framework Accelerate

---

### 7: Windows: Installation

The installation is comprised of 3 steps:

* Step 1:
  Copy the entire "include" folder to a convenient location
  and tell your compiler to use that location for header files
  (in addition to the locations it uses already).
  Alternatively, you can use the "include" folder directly.

* Step 2:
  Modify "include/armadillo_bits/config.hpp" to indicate which
  libraries are currently available on your system. For example,
  if you have LAPACK, BLAS (or OpenBLAS), ARPACK and SuperLU present,
  uncomment the following lines:

    #define ARMA_USE_LAPACK  
    #define ARMA_USE_BLAS  
    #define ARMA_USE_ARPACK  
    #define ARMA_USE_SUPERLU  

  If you don't need sparse matrices, don't worry about ARPACK or SuperLU.

* Step 3:
  Configure your compiler to link with LAPACK and BLAS
  (and optionally ARPACK and SuperLU).

---

### 8: Windows: Compiling and Linking

Within the "examples" folder, there is an MSVC project named "example1_win64"
which can be used to compile "example1.cpp". The project needs to be compiled as a
64 bit program: the active solution platform must be set to x64, instead of win32.

The MSVC project was tested on 64 bit Windows 7 with Visual C++ 2012.
You may need to make adaptations for 32 bit systems, later versions of Windows
and/or the compiler. For example, you may have to enable or disable
ARMA_BLAS_LONG and ARMA_BLAS_UNDERSCORE defines in "armadillo_bits/config.hpp".

The folder "examples/lib_win64" contains baseline (unoptimised) LAPACK and BLAS
libraries compiled for 64 bit Windows. The compilation was done by a third party.
USE AT YOUR OWN RISK. The compiled versions of LAPACK and BLAS were obtained from:
  http://ylzhao.blogspot.com.au/2013/10/blas-lapack-precompiled-binaries-for.html

Faster and/or alternative implementations of BLAS and LAPACK are available:
  * http://www.openblas.net/
  * http://icl.cs.utk.edu/lapack-for-windows/lapack/
  * http://software.intel.com/en-us/intel-mkl/

OpenBLAS and Intel MKL are generally the fastest replacements for both BLAS and LAPACK.

**Caveat:** 
for any high performance scientific/engineering workloads,
we strongly recommend using a Linux based operating system:
  * Fedora  http://fedoraproject.org/
  * Ubuntu  http://www.ubuntu.com/
  * CentOS  http://centos.org/

---

### 9: Support for OpenBLAS and Intel MKL

Armadillo can use OpenBLAS or Intel Math Kernel Library (MKL) as high-speed
replacements for BLAS and LAPACK. In essence this involves linking with the
replacement libraries instead of BLAS and LAPACK.

You may need to make minor modifications to include/armadillo_bits/config.hpp
to make sure Armadillo uses the same integer sizes and style of function names
as used by the replacement libraries. Specifically, you may need comment or uncomment
the following defines:

    ARMA_USE_WRAPPER  
    ARMA_BLAS_CAPITALS  
    ARMA_BLAS_UNDERSCORE  
    ARMA_BLAS_LONG  
    ARMA_BLAS_LONG_LONG  

See the documentation for more information on the above defines.

On Linux-based systems, MKL might be installed in a non-standard location
such as /opt which can cause problems during linking.  Before installing
Armadillo, the system should know where the MKL libraries are located.
For example, /opt/intel/mkl/lib/intel64/.  This can be achieved by setting
the LD_LIBRARY_PATH environment variable, or for a more permanent solution,
adding the directory locations to /etc/ld.so.conf.  It may also be possible
to store a text file with the locations in the /etc/ld.so.conf.d directory.
For example, /etc/ld.so.conf.d/mkl.conf.  If you modify /etc/ld.so.conf
or create /etc/ld.so.conf.d/mkl.conf, you will need to run /sbin/ldconfig
afterwards.

Below is an example of /etc/ld.so.conf.d/mkl.conf
where Intel MKL is installed in /opt/intel

    /opt/intel/lib/intel64  
    /opt/intel/mkl/lib/intel64  

If you have MKL installed and it is persistently giving problems
during linking, you can disable Armadillo's support for MKL by editing
the CMakeLists.txt file, deleting CMakeCache.txt and re-running
the CMake based installation. Comment out the lines containing:

    INCLUDE(ARMA_FindMKL)  
    INCLUDE(ARMA_FindACMLMP)  
    INCLUDE(ARMA_FindACML)  

---

### 10: Support for ATLAS

Armadillo can use the ATLAS library for faster versions of a subset
of LAPACK and BLAS functions. LAPACK should still be installed to
obtain full functionality.

Caveat: the minimum recommended version of ATLAS is 3.10;
earlier versions (such as 3.6 and 3.8) can produce incorrect
results and/or corrupt memory, leading to random crashes.

---

### 11: Support for C++11 / C++14 Features

Armadillo works with compilers supporting the older C++98 and C++03 standards,
as well as the newer C++11 and C++14 standards.

Armadillo will enable extra features (such as move constructors)
when a C++11/C++14 compiler is detected. You can also force Armadillo
to make use of C++11 features by defining ARMA_USE_CXX11 before
`#include <armadillo>` in your code.

You may need to explicitly enable C++11 mode in your compiler.
For example, use the -std=c++11 or -std=c++14 options in gcc & clang.

**Caveat:** use of the C++11 "auto" keyword is not recommended with Armadillo
objects and expressions. Armadillo has a template meta-programming framework
which creates lots of short lived temporaries that are not handled by auto.

---

### 12: Support for OpenMP

Armadillo can use OpenMP to automatically speed up computationally
expensive element-wise functions such as exp(), log(), cos(), etc.
This requires a C++11/C++14 compiler with OpenMP 3.1+ support.

When using gcc or clang, use the following options to enable both
C++11 and OpenMP:  -std=c++11 -fopenmp

Caveat: when using gcc, use of -march=native in conjunction with -fopenmp
may lead to speed regressions on recent processors.

---

### 13: Documentation

The documentation for Armadillo functions and classes is available at:  
http://arma.sourceforge.net/docs.html

The documentation is also in the "docs.html" file in this folder,
which can be viewed with a web browser.

---

### 14: API Stability and Versioning

Each release of Armadillo has its public API (functions, classes, constants)
described in the accompanying API documentation (docs.html) specific
to that release.

Each release of Armadillo has its full version specified as A.B.C,
where A is a major version number, B is a minor version number,
and C is a patch level (indicating bug fixes).

Within a major version (eg. 7), each minor version has a public API that
strongly strives to be backwards compatible (at the source level) with the
public API of preceding minor versions. For example, user code written for
version 7.100 should work with version 7.200, 7.300, 7.400, etc. However,
as later minor versions may have more features (API extensions) than
preceding minor versions, user code specifically written for version 7.400
may not work with 7.300.

An increase in the patch level, while the major and minor versions are retained,
indicates modifications to the code and/or documentation which aim to fix bugs
without altering the public API.

We don't like changes to existing public API and strongly prefer not to break
any user software. However, to allow evolution, we reserve the right to
alter the public API in future major versions of Armadillo while remaining
backwards compatible in as many cases as possible (eg. major version 8 may
have slightly different public API than major version 7).

**CAVEAT:** any function, class, constant or other code _not_ explicitly described
in the public API documentation is considered as part of the underlying internal
implementation details, and may change or be removed without notice.
(In other words, don't use internal functionality).

---

### 15: Bug Reports and Frequently Asked Questions

Armadillo has gone through extensive testing and has been successfully
used in production environments. However, as with almost all software,
it's impossible to guarantee 100% correct functionality.

If you find a bug in the library or the documentation, we are interested
in hearing about it. Please make a _small_ and _self-contained_ program
which exposes the bug, and then send the program source and the bug description
to the developers. The small program must have a main() function and use only
functions/classes from Armadillo and the standard C++ library (no other libraries).

The contact details are at:  
http://arma.sourceforge.net/contact.html

Further information about Armadillo is on the frequently asked questions page:  
http://arma.sourceforge.net/faq.html

---

### 16: MEX Interface to Octave/Matlab

The "mex_interface" folder contains examples of how to interface
Octave/Matlab with C++ code that uses Armadillo matrices.

---

### 17: Related Software Using Armadillo

* MLPACK: extensive library of machine learning algorithms  
  http://mlpack.org

* ensmallen: C++ library of numerical optimisation methods  
  http://ensmallen.org/

* SigPack: C++ signal processing library  
  http://sigpack.sourceforge.net

* RcppArmadillo: integration of Armadillo with the R system and environment  
  http://dirk.eddelbuettel.com/code/rcpp.armadillo.html
