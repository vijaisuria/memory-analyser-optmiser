# OPTIMISED MEMORY ALLOCATOR AND ANALYSER

![OS Linux](https://img.shields.io/badge/OS-Linux-blue)
![OS MacOS](https://img.shields.io/badge/OS-MacOs-blue)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/memray)
![PyPI - Implementation](https://img.shields.io/pypi/implementation/memray)
![PyPI](https://img.shields.io/pypi/v/memray)

Memory management is a crucial part of any operating system (OS), as it is responsible for handling memory allocation and deallocation. The operating system provides an abstraction layer between the application programs and the physical hardware. Garbage collection is the automatic management of memory allocation and deallocation in programming languages like Java and Python, which is handled by the virtual machine or interpreter. This project aims at profiling the memory resources and keeps track and reports the allocation in C/C++ and Rust using python. It helps us in analysing allocations in applications to help discover the cause of high memory usage, finding native memory leaks made by also finding hotspots in code that cause a lot of allocate ons. The main advantage is that it can be easily integrated with Linux and MacOS either via Command line or GUI (Graphical User Interface).

Notable features:
- Traces every function call so it can accurately represent the call stack, unlike sampling profilers.
- Also handles native calls in C/C++ libraries so the entire call stack is present in the results.
- Blazing fast! Profiling slows the application only slightly. Tracking native code is somewhat slower,
  but this can be enabled or disabled on demand.
- It can generate various reports about the collected memory usage data, like flame graphs.
- Works with Python threads.
- Garbage Collector : It will automatically detect and free memory that is no longer being used by a program. 
- Works with native-threads (e.g. C++ threads in C extensions).

It can help with the following problems:
- Analyze allocations in applications to help discover the cause of high memory usage.
- Find memory leaks.
- Find hotspots in code that cause a lot of allocations.

> **Note**
> Our Project only works on Linux and MacOS, and cannot be installed on other platforms.

# Installation

## Prerequsite
- Python & C++
- support glibc and must libc
- Linux and Mac Environment
- libunwind (for Linux) & liblz4 (Mac)

## Steps

Once downloading and extracting our project, go to location where the project exists
Check your package manager on how to install the dependencies
`apt-get install libunwind-dev liblz4-dev` in Debian-based systems
or `brew install lz4` in MacOS.

```shell
    cd memray-main
    python3 -m venv ../memray-env/  t
```

Create the virtual environment for safe and secure operations, building project files

```shell
    source ../memray-env/bin/activate
    python3 -m pip install --upgrade pip
    python3 -m pip install -e . -r requirements-test.txt -r requirements-extra.tx
```

After the successful deployment, To install vkMan, a real-time monitoring of various aspects of your system such as CPU, memory, disk, network usage etc via a web interface or command line interface. It is easy to install and use and can be customized to show only the information that you are interested in.

```shell
    $ cd vkMan-*
    # python setup.py install
```

# USAGE

```
usage: memray [-h] [-v] {run,flamegraph,table,live,tree,parse,summary,stats} ...

Run `memray run` to generate a memory profile report, then use a reporter command
such as `memray flamegraph` or `memray table` to convert the results into HTML.

Example:

    $ python3 -m memray run -o output.bin my_script.py
    $ python3 -m memray flamegraph output.bin

positional arguments:
  {run,flamegraph,table,live,tree,parse,summary,stats}
                        Mode of operation
    run                 Run the specified application and track memory usage
    flamegraph          Generate an HTML flame graph for peak memory usage
    table               Generate an HTML table with all records in the peak memory usage
    live                Remotely monitor allocations in a text-based interface
    tree                Generate a tree view in the terminal for peak memory usage
    parse               Debug a results file by parsing and printing each record in it
    summary             Generate a terminal-based summary report of the functions that allocate most memory
    stats               Generate high level stats of the memory usage in the terminal

optional arguments:
  -h, --help            Show this help message and exit
  -v, --verbose         Increase verbosity. Option is additive and can be specified up to 3 times

```

<hr>

##vkMan

For the standalone mode, just run:

``` console
$ ./vkMan.sk
```

For the Web server mode, run:

``` console
$ ./vkMan.sk -w
```

and enter the URL `http://<ip>:61208` in your favorite web browser.

For the client/server mode, run:

``` console
$ ./vkMan.sk -s
```

on the server side and run:

``` console
$ ./vkMan.sk -c <ip>
```

on the client one.

You can also detect and display all Glances servers available on your
network or defined in the configuration file:

``` console
$ ./vkMan.sk --browser
```

You can also display raw stats on stdout:

``` console
$ ./vkMan.sk --stdout cpu.user,mem.used,load
cpu.user: 30.7
mem.used: 3278204928
load: {'cpucore': 4, 'min1': 0.21, 'min5': 0.4, 'min15': 0.27}
cpu.user: 3.4
mem.used: 3275251712
load: {'cpucore': 4, 'min1': 0.19, 'min5': 0.39, 'min15': 0.27}
...
```

or in a CSV format thanks to the stdout-csv option:

``` console
$ ./vkMan.sk --stdout-csv now,cpu.user,mem.used,load
now,cpu.user,mem.used,load.cpucore,load.min1,load.min5,load.min15
2018-12-08 22:04:20 CEST,7.3,5948149760,4,1.04,0.99,1.04
2018-12-08 22:04:23 CEST,5.4,5949136896,4,1.04,0.99,1.04
...
```

or in a JSON format thanks to the stdout-json option (attribute not
supported in this mode in order to have a real JSON object in output):

``` console
$ ./vkMan.sk --stdout-json cpu,mem
cpu: {"total": 29.0, "user": 24.7, "nice": 0.0, "system": 3.8, "idle": 71.4, "iowait": 0.0, "irq": 0.0, "softirq": 0.0, "steal": 0.0, "guest": 0.0, "guest_nice": 0.0, "time_since_update": 1, "cpucore": 4, "ctx_switches": 0, "interrupts": 0, "soft_interrupts": 0, "syscalls": 0}
mem: {"total": 7837949952, "available": 2919079936, "percent": 62.8, "used": 4918870016, "free": 2919079936, "active": 2841214976, "inactive": 3340550144, "buffers": 546799616, "cached": 3068141568, "shared": 788156416}
...
```
