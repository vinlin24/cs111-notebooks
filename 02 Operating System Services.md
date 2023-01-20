# Lecture 02 (01/12/2022): Operating System Services


## The OS and Abstractions


One major function of an OS is to offer **abstract** versions of **physical** resources.

* Processes (abstraction) ~ use of CPU/RAM (physical)
* Files (abstraction) ~ flash drives (physical)

These abstractions are more *useful* for application programmers to work with.

* Easier to use than the original resources
* Compartmentalize/encapsulate complexity
* Eliminate behavior that is irrelevant to the user
* Create more convenient behavior

We can *generalize* abstractions to make many different types of hardware and software *appear* the same. This way, many applications can deal with a single common class. This usually involves a common unifying model.

The popular **portable document format (PDF)** is an example that unifies document formatting for printers. Also, printer drivers make different printers look the same.


## Types of OS Resources


### Serially Reusable Resources


Used by multiple clients, but only one at a time (**time multiplexing**). The client currently using it has **exclusive use**. This requires **access control** and **graceful transitions** from one user to the next.


Examples:

* Printers
* Speakers
* Bathrooms!

**What is a graceful transition?**

* No incomplete operations that finish *after* a transition. The first user has to be completely done before moving on the second.
* Every subsequent user should find a resource in a "like new" condition, with no traces of data or state left over from the first user.

Information about a process that is stopped but needs to start back up again is stored in memory somewhere. This is necessary because sometimes a process is stopped to make room for another process on the same core. The former process should be reinitialized with its stack pointer, etc. when it's started up again on that core or even another core.


### Partitionable Resources


Divided into disjoint pieces for multiple clients (**spatial multiplexing**). This also needs **access control** to ensure:

* **Containment**: you cannot access resources *outside* of your **partition.**
* **Privacy**: nobody else can access resources in *your* partition.

Examples:

* RAM
* Hard disk drive
* Hotel rooms!

Still needs graceful transitions because most partitionable resources aren't permanently allocates. As long as a resource is not "yours", sooner or later it's likely to become someone else's, so a transition is required.


### Shareable Resources


Usable by multiple concurrent clients. Clients don't "wait" for acess to a resource, nor do they "own"  a particular subset of the resource. The clients use the resources *at the same time.*

These *appear* as (effectively) limitless resources.

Examples:

* Copy of the OS, shared by all processes
* Air in a room, shared by occupants!

These typically do not need graceful transitions because:

* Shareable resources usually do not *change state* or it isn't "reused". It's **read-only**.
* We never have to clean up what doesn't get dirty, like an execute-only copy of the OS

> **TIP**: Design your system to *maximize* shareable resources.


## Trends in Operating Systems


Their role has fundamentally changed, ultimately because it's to keep up with what users want. Applications have become more complex with more complex internal behavior, interfaces, and interaction with other software.


* **BEFORE**: shepherding the use of hardware.
* **AFTER**: shielding the applications from hardware (abstractions), providing powerful application computing platform, becoming a sophisticated "traffic cop".

Something that hasn't changed is that they still sit between applications and hardware. We still understand them through services that they provide, including:

* Capabilities you add
* Applications they enable
* Problems they eliminate

> Remember the fundamental purpose of the OS is to *help* with complexity.


### Convergence of OSes


OSes are expensive to build and maintain, so the business has a high price of entry. It must also support all the apps the users want for them to choose the OS over other options.

This had led to a convergence of OSes. There are only a handful of widely used OSes, namely (the big three lol):

* Windows (1985)
* MacOS (which is itself a Unix-like system) (1984)
* Linux (which itself descends from Unix as well) (1991)

Among a few special purpose ones like real time and embedded system OSes, like FreeBSD, QNX, and TinyOS.

The big 3 all descend from the same old models developed about 30 years prior.


## OS Services


> All about abstractions!

Basic categories of abstractions:

* CPU/memory abstractions
* Persistent storage abstractions
* Other I/O abstractions

Services: higher level abstractions:

* Cooperating parallel processes
* Security
* User interface

Services: under the covers:

* Enclosure management (monitoring the physical appliances, like managing the computer's fans!)
* Software updates and configuration registry
* Dynamic resource allocation and scheduling
* Networks, protocols, and domain services
