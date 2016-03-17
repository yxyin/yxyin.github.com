---
layout: post
title: Performance Tunning Tips
tags: 性能测试
categories: 性能测试
---

## Performance Tunning Tips ##

 - **Performance tuning** is usually about focusing on a few key variables. We will highlight the most
common tuning knobs that can often improve the speed of the average application by 200% or
more relative to the default configuration. The first step, however, should be to use and be
guided by the tools and methodologies. Gather data, analyze it and create hypotheses: then test
your hypotheses. Rinse and repeat. As Donald Knuth says: "Programmers waste enormous
amounts of time thinking about, or worrying about, the speed of noncritical parts of their
programs, and these attempts at efficiency actually have a strong negative impact when
debugging and maintenance are considered. We should forget about small efficiencies, say
about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up
our opportunities in that critical 3%. A good programmer will not be lulled into complacency by
such reasoning, he will be wise to look carefully at the critical code; but only after that code has
been identified. It is often a mistake to make a priori judgments about what parts of a program
are really critical, since the universal experience of programmers who have been using
measurement tools has been that their intuitive guesses fail." (Donald Knuth, Structured
Programming with go to Statements, Stanford University, 1974, Association for Computing
Machinery)
 - There is a seemingly daunting number of tuning knobs. We try to document everything in detail
in case you hit a problem in that area; however, unless you are trying to squeeze out every last
drop of performance, we **do not recommend a close study of every point**.
 - In general, we advocate a **bottom-up** approach. For example, with a typical WebSphere
Application Server application, start with the operating system, then Java, then WAS, then the
application, etc. Ideally, investigate these at the same time. The main goal of a performance
tuning exercise is to iteratively determine the bottleneck restricting response times and
throughput. For example, investigate operating system CPU and memory usage, followed by
Java garbage collection usage and/or thread dumps/sampling profilers, followed by WAS PMI,
etc.
 - One of the most difficult aspects of performance tuning is understanding whether or not the
architecture of the system, or even the test itself, is valid and/or optimal.
 - Meticulously describe and track the problem, each test and its results.
 - Use basic statistics (minimums, maximums, averages, medians, and standard deviations) instead
of spot observations.
 - When benchmarking, use a repeatable test that accurately models production behavior, and
avoid short term benchmarks which may not have time to warm up.
 - Take the time to automate as much as possible: not just the testing itself, but also data gathering
Page 454
and analysis. This will help you iterate and test more hypotheses.
 - Make sure you are using the latest version of every product because there are often performance
or tooling improvements available.
 - When researching problems, you can either analyze or isolate them. Analyzing means taking
particular symptoms and generating hypotheses on how to change those symptoms. Isolating
means eliminating issues singly until you've discovered important facts. In general, we have
found through experience that analysis is preferable to isolation.
 - Review the full end-to-end architecture. Certain internal or external products, devices, content
delivery networks, etc. may artificially limit throughput (e.g. Denial of Service protection),
periodically mark services down (e.g. network load balancers, WAS plugin, etc.), or become
saturated themselves (e.g. CPU on load balancers, etc.).
