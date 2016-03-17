---
layout: post
title: Java Tunning Tips
tags: 性能测试 JVM
categories: 性能测试 JVM
---


1. Tune the maximum Java heap size (-Xmx):
 + Enable verbose garbage collection (-verbose:gc) which prints statistics on garbage
collection to files and generally has an overhead less than 1%. Use a tool such as the
IBM Garbage Collection and Memory Visualizer to analyze the verbosegc output. The
proportion of time spent in garbage collection versus application processing time should
generally be less than 10% and ideally less than 1%.
 +  **Garbage collection** will adapt heap size to keep occupancy **between 40% and 70%**. Heap
occupancy over 70% causes frequent GC cycles... Heap occupancy below 40% means
infrequent GC cycles, but cycles longer than they needs to be... The maximum heap size
setting should therefore be 43% larger than the maximum occupancy of the application.
2. Consider the particular type of garbage collector to use (see the comparison table in either the
IBM Java or Oracle/HotSpot Java chapters).
3. Ensure there is no memory leak with long running tests.
4. If using a generational collector such as IBM gencon/balanced or the Oracle JVM:
 + Ensure tests run through full/tenured collections and ensure those pause times are not too
long.
 + Ensure that there is a sawtooth pattern in the heap usage after collection. Otherwise, the
heap size may be too small or the nursery too big.
 + Generally, the sawtooth should drop about 25% of the heap size on full collections.
5. Total pause times over a few seconds should be routinely investigated.
6. Use a profiler such as **IBM Java Health Center** or **Java Mission Control** with a particular focus
on the profiling and lock contention analysis. Otherwise, use periodic thread dumps to review
JVM activity with the **IBM WAIT** or **IBM Thread and Monitor Dump Analyzer** tools.
7. Object allocation failures for objects greater than **5MB** should generally be investigated.
8. Take a system dump or HPROF heapdump during peak activity and review it with the IBM
Memory Analyzer Tool to see if there are any areas in the heap for optimization.
9. Review the stderr and stdout logs for any errors, warnings, or high volumes of messages (e.g.
OutOfMemoryErrors).
10. If running multiple JVMs on the same machine, consider pinning JVMs to sets of processor
cores and tuning ***-Xgcthreads/-XcompilationThreads*** or ***-XX:ParallelGCThreads***.
11. In general, if memory usage is very flat and consistent, it may be optimal to fix **-Xms = -Xmx**.
For widely varying heap usage, -Xms < -Xmx is generally recommended. You may get the best
of both worlds by setting -Xms to the lowest steady state memory usage, -Xmaxf1.0 to
eliminate shrinkage, -Xminf to avoid compaction before expansion, and -Xmine to reduce
expansions.
12. Request a thread dump and search its output for "deadlock" to ensure that no threads are
deadlocked (thus reducing throughput).
13. If using the IBM Java Runtime Environment:
 + In most cases, the gencon garbage collection policy works best, with the key tuning
being the maximum heap size (-Xmx) and maximum nursery size (-Xmn).
 + If physical memory allows, increase the size of the shared class cache (-Xshareclasses).
 + Test with large pages (-Xlp). These are enabled by default in recent versions, but may
require operating system configuration for full enablement.
 + Test with -Xaggressive.
 + Test with -XtlhPrefetch.
 + 6. Consider enabling **IBM Java Health Center** (-Xhealthcenter) by default so that you can
attach to particular processes if they start to have trouble.
 + If using IBM Java >= 7 SR3, the IBM JCE security provider and recent Intel, AMD, or
POWER >= 8 CPUs, then AESNI hardware acceleration for AES encryption and
decryption can be exploited with -Dcom.ibm.crypto.provider.doAESInHardware=true.
This can reduce TLS overhead by up to 35%.
 + If the static IP address of the node on which Java is running is unlikely to change, use
-Dcom.ibm.cacheLocalHost=true to reduce localhost lookup time.
 + Take a javacore thread dump and review the Java arguments (UserArgs) and
Environment Variables sections for uncommon or debug options.
14. If using the Oracle Java Runtime Environment:
 + In most cases, the -XX:+UseParallelOldGC garbage collection policy works best, with
the key tuning being the maximum heap size (-Xmx) and maximum new generation size
(-XX:MaxNewSize).
 + Set **-XX:+HeapDumpOnOutOfMemoryError**.
 + When using ergonomics, consider tuning **-XX:MaxGCPauseMillis** and
**-XX:GCTimeRatio**.
 + When fine-tuning is required, consider disabling ergonomics (-XX:-AdaptiveSizePolicy)
and tune the SurvivorRatio (-XX:SurvivorRatio).
15. In most cases, sampling profilers are used first and tracing profilers are only used for fine
grained tuning or deep dive analysis.
16. Analyze any methods that use more than 1% of the reported time in themselves.
17. Analyze any methods that use more than 10% of the reported time in themselves and their
children.
18. Analyze any locks that have large contention rates, particularly those with long average hold
times.