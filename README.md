# Hurricane Real-time Processing

You may refer to [Book Case](https://github.com/samblg/hurricane/tree/book_case) for the code of book and the first workable source code.

##0.6.1 (master branch)
This branch includes the following major updates:

- New order preserving mechanism. (Message distribution in managers is in parallel way.)
- New features in kake build system. (Isolation of project and platform configurations, completed log mechanism and support of build/install/clean commands.)
- kqueue enhancment in meshy network library.

##0.6.2
- New APIs in meshy network library.
- OpenSSL support in meshy network library.
- Windows server platform support. (Providing Microsoft Visual Studio projects.)

##Brief Introduction
Hurricane is a C++ based distributed real-time processing system.
Different from the batch processing system like Apache Hadoop, 
Hurricane uses stream model to process data. It also supports multi-language interfaces, 
such as Python, JavaScript, Java and Swift.

We imitate the interface of Apache Storm and simplify it, 
so the developer familiar with Storm can learn the Hurricane easily.

## Basic concepts
### Topology
The logic for a realtime application is packaged into a Hurricane topology. 
A Hurricane topology is analogous to a MapReduce job. 
One key difference is that a MapReduce job eventually finishes, 
whereas a topology runs forever. 

### Stream
The stream is an important abstraction in Hurricane. 
A stream is an unbounded sequence of tuples that is processed and created in parallel in a distributed fashion.
Streams are defined with a schema that names the fields in the stream's tuples.

### Tuple
Tuple is the data unit transferred in stream. 
The spout and bolt need to use tuple to organize the data.
Tuples can contain integers, longs, shorts, characters, floats, doubles and strings.

### Spout
A spout is a source of streams in a topology.
Generally spouts will read tuples from an external source and emit them into the topology.
Spouts can either be reliable or unreliable.
A reliable spout is capable of replaying a tuple if it failed to be processed by Hurricane, whereas an unreliable spout forgets about the tuple as soon as it is emitted.

### Bolt
All processing in topologies is done in bolts. 
Bolts can do anything from filtering, functions, aggregations, joins, talking to databases, and more.

##Installation
###Dependencies
Hurricane depends on Meshy network library (libmeshy, a transportation layer library designed for Hurricane real-time processing), you could find Meshy in deps folder, build Meshy before starting to build Hurricane. 
Hurricane supports to be built by Makefile (gmake) and Kakefile (Kake). Refer to the section "Build with Kake" for more details on how to build and install Hurricane.

### Build Hurricane using Makefile
For the sake of convenience of Linux users' usage, we provided Makefile to build Hurricane.
It's very simple to build with Makefile, simply type the following command:

make

### Build Hurricane using gmake
First the jvm lib which is needed when linking objects and the include path for jni.h should be specified in corresponding Makefile.deps. For now modify target/Makefile.deps

```
    JNI_INCLUDE := -I"/opt/jdk1.8.0_111/include" -I"/opt/jdk1.8.0_111/include/linux"
    JNI_LIB := -L"/opt/jdk1.8.0_111/jre/lib/amd64/server"
```

Enter target/build/linux/x64/Release/build and type:

    make install

The nimbus and supervisor will be built into target/bin/linux/x64/Release. The demo project will submit a sample word count topololgy.

## Get Started
After the installation, you can write a simple topology described in [docs/introduction.md](https://github.com/samblg/hurricane/blob/master/docs/introduction.md). Then submit the output shared library to Hurricane.
