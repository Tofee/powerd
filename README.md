powerd
======
Powerd is one of the primary daemons that is started when webOS boots. It is responsible for monitoring battery parameters like temperature, current, voltage and other inputs, and making decisions about battery charging. It interfaces with the underlying hardware using the Nyx client library, talking to the battery and charger modules for the platform. At the same time it exposes the battery and charging information to the upper layers through the Luna Service Bus. Powerd also has the capability to run the necessary CTIA checks for temperature limits on the platform. 

How to Build on Linux
=====================

## Dependencies

Below are the tools and libraries (and their minimum versions) required to build powerd:

* cmake 2.6
* gcc 4.3
* glib-2.0 2.16.6
* make (any version)
* openwebos/cjson 1.8.0
* openwebos/luna-service2 3.0.0
* openwebos/nyx-lib 2.0.0 RC 2
* pkg-config 0.22


## Building

Once you have downloaded the source, execute the following to build it:

    $ mkdir BUILD
    $ cd BUILD
    $ cmake ..
    $ make
    $ sudo make install

The header files will be installed under

    /usr/local/include/powerd

the libraries and pkg-config file under

    /usr/local/lib

the daemon under

    /usr/local/sbin

the default preferences file under

    /usr/local/etc/default

and the upstart script under

    /usr/local/etc/event.d

You can install it elsewhere by supplying a value for _CMAKE\_INSTALL\_PREFIX_ when invoking _cmake_. For example:

    $ cmake -D CMAKE_INSTALL_PREFIX:STRING=$HOME/projects/openwebos ..
    $ make
    $ make install
    
will install the files in subdirectories of $HOME/projects/openwebos instead of subdirectories of /usr/local. 

Specifying _CMAKE\_INSTALL\_PREFIX_ also causes the pkg-config files under it to be used to find headers and libraries. To have _pkg-config_ look in a different tree, set the environment variable PKG_CONFIG_PATH to the path to its _lib/pkgconfig_ subdirectory.

## Uninstalling

From the directory where you originally ran _make install_, invoke:

    $ sudo xargs rm < install_manifest.txt

## Generating documentation

The tools required to generate the documentation are:

* doxygen 1.6.3
* graphviz 2.20.2

Once you have run _cmake_, execute the following to generate the documentation:

    $ make docs

To view the generated HTML documentation, point your browser to

    doc/html/index.html

## Linking against libpowerd

If your system has pkg-config then you can just add this to your makefile:

    CFLAGS += $(shell pkg-config --cflags powerd)
    LDFLAGS += $(shell pkg-config --libs powerd)

# Copyright and License Information

All content, including all source code files and documentation files in this repository are: 

 Copyright (c) 2007-2012 Hewlett-Packard Development Company, L.P.

All content, including all source code files and documentation files in this repository are:
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this content except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

