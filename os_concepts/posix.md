[Home](../README.md)

### POSIX    
The Portable Operating System Interface (POSIX) is an IEEE standard that helps compatibility and portability 
between operating systems. Theoretically, POSIX compliant source code should be seamlessly portable. In the 
real world, application transition often runs into system specific issues. But POSIX compliance makes it simpler 
to port applications which can result in time savings. So developers should get acquainted with the fundamentals 
of this widely used standard.

**History of POSIX**  
Early programmers had to rewrite their applications from scratch for each new computer model. But the IBM System/360 
changed that. In 1964, it introduced the operating system OS/360. IBM started to use the same hardware architecture 
to enable the new models to reuse the same operating system. The presence of a common OS across multiple machines 
set up the first stage for application portability.  

In the late 1960s, the arrival of UNIX opened up new possibilities. AT&T’s Bell Labs was responsible for the initial 
development of this new operating system. It could run across machines from multiple vendors. But UNIX started to fork 
into various flavors. Besides the AT&T’s System V, there were Berkeley Software Distribution (BSD), Xenix and more. 
It wasn’t easy to port across these flavors. The promise of application portability hit a road bump. In the coming 
decades, the introduction of new operating systems would only make it more complex to port applications across 
hardware, operating systems, and vendors.  

POSIX standard was developed in the 1980s to resolve the portability issue. The standard was defined based on System V 
and BSD Unix. POSIX does not define the operating system, it only defines the interface between an application and an 
operating system. The programmers have the freedom to write their OS and application anyway they want as long as the 
interface between the two is honored. Because POSIX is independent of hardware, operating system or vendor, it’s 
easier to achieve application portability.  

The first POSIX standard was released in 1988. Formally, it was called IEEE Standard 1003.1-1988 Portable Operating 
System Interface for Computer Environments”. In 1990, an international version of the same standard with slight 
variations was released as ISO/IEC 9945-1:1990 Information technology — Portable Operating System Interface 
(POSIX) — Part 1: System Application Program Interface (API).  

Initially, POSIX was divided into multiple standards:
* POSIX.1: Core Services
* POSIX.1b: Real-time extensions
* POSIX.1c: Threads extensions
* POSIX.2: Shell and Utilities  

After 1997, the Austin Group brought all the standard under a single umbrella. Since then, the versions POSIX.1-2001 
(also known as IEEE Std 1003.1-2001), POSIX.1-2004 (also known as IEEE Std 1003.1-2004) and POSIX.1-2008 (also known 
as IEEE Std 1003.1-2008) have been released. Examples of some POSIX-compliant systems are AIX, HP-UX, Solaris, 
and MacOS (since 10.5 Leopard). On the other hand, Android, FreeBSD, Linux Distributions, OpenBSD, VMWare, etc., 
follow most of the POSIX standard, but they are not certified.  

**Basics of POSIX**  
POSIX.1-2008 standard deals with four major areas:  
```markdown
Base Definition Volume      : General terms, concepts, and interfaces.
Systems Interfaces Volume   : Definitions of system service functions and subroutines. Also, includes portability, error
                              handling and error recovery.
Shell and Utilities Volume  : Definition of interfaces of any application to command shells and common utility programs.
Rationale Volume            : Contains information and history about added or discarded features and the reasonings of 
                              the decisions.
```
The standard doesn’t cover graphical interfaces, database interfaces, object/binary code portability, system 
configurations, I/O considerations or resource availability.

**Some of the guiding principles behind POSIX design are**:  
* POSIX is created to make application portability easier. So it’s not for UNIX systems only. Non-UNIX systems can be 
  POSIX-compliant too.
* The standard doesn’t dictate the development of the application or the operating system. It only defines the contract
  between them.
* POSIX-compliant application source code should be able to run across many systems because the standard is defined
  at the source code level. However, the standard doesn’t guarantee any object or binary code level portability.
  So the binary executable may not run even on similar machines with identical hardware and operating systems.
  Only source code portability is addressed in the standard.
* POSIX is written in terms of Standard C. But developers can implement it in any language they like.
* The standard only deals with aspects of the operating system that interacts with applications.
* The standard is kept succinct in terms of length and broad in terms of scope to cover a large array of systems.
* POSIX was designed to simplify portability. So it will save time and money in the long run. However, if your 
  applications are not POSIX-compliant, it might require significant time and resource investment at the beginning.

**POSIX Application Development**  
The purpose of POSIX was to improve portability. When your source code follows the standard, you can compile and run 
the code on a different machine easily. However, if POSIX is defined as a general requirement for an application, it 
can cause confusion. The full POSIX standard is 4000-plus pages with more than 1350 interfaces. It doesn’t make sense 
to implement everything. So each project should define the aspects of POSIX that will meet particular requirements.  

There are misconceptions in the development community that POSIX standard is old and irrelevant. It is not true. POSIX 
is a living document that is being regularly updated by the Austin Group. Anyone can join the group and participate in 
improving the standard. The standard is used actively in today’s servers, workstations, routers, mobile devices, 
embedded systems and more. It is used for UNIX and Linux machines.

However, developers should be aware that POSIX standard has problems. You can report any bug you discover to the Austin
Group and it will be looked into for the next revision.

**Conclusion**  
POSIX might seem daunting at first. Still, application developers should get acquainted with the basics as it will pop 
up as a requirement from time to time. Due to the large scope of the standard, it’s not possible to become an expert 
on the full document. Developers can reach out to the UNIX and Linux communities to learn more. The communities can 
answer your questions and give you a better sense of what part of the standard will be relevant to your project.

References:
* https://linuxhint.com/posix-standard/
* https://kb.iu.edu/d/agjv
* https://pubs.opengroup.org/onlinepubs/9699919799/