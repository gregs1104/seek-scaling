Introduction
============

``seek-scaling`` automates running the sysbench seek tests and plotting
the results.  It is currently compatible with Linux only.  The main
non-portable requirement is the fact that it clears the operating
system cache between each test run in a Linux-specific way.

Customizing the program
=======================

Currently all of the input parameters to the program are hard-coded into
the scripts.  Edit the following:

 * seek-scaling:  Set the description of the device being tested (DESCR),
   what filename to store the text format results (FILENAME), and what to name
   the graph of the results (GRAPH)
 * seek-scaling-sysbench:  Set the size of the data set (GBSIZE) and what
   type of test to run (MODE).  

You can also adjust parameters like the number of threads and the amount of
time to run the test, but changing those shouldn't be necessary for most
tests.

The useful testing modes for seek-scaling are:

 * rndrd: random read (the default)
 * rndwr: random write 
 * rndrw: combined random read/write 
 * seqwr: sequential write 
 * seqrd: sequential read 

The program assumes you have sysbench installed in the 0.4 subdirectory of
your home directory.  Installation instructions for tha tprogram are below.

Installing sysbench
===================

seek-scaling requires that the sysbench program be installed.
The stable 0.4 version is recommended.  The packaged releases
of sysbench are difficult to compile on many systems.  Those
problems are most easily resolved by installing the latest
development snapshot instead, where the build issues are
fixed.  Assuming you have the bazaar version control system
installed, the developer snapshot can be installed into your
home directory like this::

  cd
  bzr checkout https://code.launchpad.net/~sysbench-developers/sysbench/0.4/
  cd 0.4
  ./autogen.sh
  ./configure --without-mysql
  make

You don't need to install sysbench to use it for seek-scaling.  Whether or not
the included by default MySQL support is installed in sysbench doesn't matter
to the program either.

If your server doesn't/can't have bazaar installed, you might archive the
source code from a system that does and copy it over, such as:

  cd
  bzr checkout https://code.launchpad.net/~sysbench-developers/sysbench/0.4/
  tar cvfz sysbench-0.4.tar.gz 0.4
  scp sysbench-0.4.tar.gz user@testhost:
  ssh user@testhost
  tar xvfz sysbench-0.4.tar.gz

And then follow the above instructions to compile the program.

TODO
====

seek-scaling is a rough set of scripts so far.  Plans for improving the
program include:

* Make all of the input parameters into script inputs (or perhaps a config file)

* Handle the fact that seek-scaling-sysbench must be run as root, but root's
  home directory is likely not where sysbench 0.4 is installed at, better

* When running the program multiple times, look for the test files and skip
  preparing them if found.

* Provide a proper interface to execute sysbench cleanup.

* Give examples of combining multiple files of output into a single graph.

Documentation
=============

The documentation ``README.rst`` for the program is in ReST markup.  Tools
that operate on ReST can be used to make versions of it formatted
for other purposes, such as rst2html to make a HTML version.

Contact
=======

The project is hosted at http://github.com/gregs1104/seek-scaling

If you have any hints, changes or improvements, please contact:

 * Greg Smith greg@2ndQuadrant.com

Credits
=======

Published sample seek-scaling results published benefitted from private
contributions all over the world.  Most submissions ask to remain
anonymous.

License
=======

seek-scaling is licensed under a standard 3-clause BSD license.

Copyright (c) 2011, Gregory Smith
All rights reserved.

Redistribution and use in source and binary forms, with or without 
modification, are permitted provided that the following conditions are 
met:

  * Redistributions of source code must retain the above copyright 
    notice, this list of conditions and the following disclaimer.
  * Redistributions in binary form must reproduce the above copyright 
    notice, this list of conditions and the following disclaimer in 
    the documentation and/or other materials provided with the 
    distribution.
  * Neither the name of the author nor the names of contributors may 
    be used to endorse or promote products derived from this 
    software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS 
IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED 
TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A 
PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT 
HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, 
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY 
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE 
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
