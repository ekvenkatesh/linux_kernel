# linux_kernel
Pet projects on linux kernel

Prioritized Memory Access
==========================
Developed for a course project at IIT Bombay. Details below:

Objective: Extend the notion of prioroty of a process for memory.

Details: The futuristic goal of this project is to have a mode based operation of the kernel. Applications are
categorized as belonging to one mode amongst a set of modes (gaming, entertainment, work etc.).
Depending on the selected mode, the particular set of applications is allowed prioritized access to
resources.

For example, when I want to study, I will set the mode to “work”. The OS will automatically
prioritize work related applications (which will be specified by me apriori, like, Browser, Eclipse
IDE, LibreOffice Writer etc). Even if a batch application is running in the background (such as the
download of a movie which I want to watch later, that application will be deprioritized).
Given a set of processes (pid's), with priorities, ensure that these processes get a chunk of the
resources (memory, IO time) irrespective of load of the system.

Approach: I now give details of how to prioritize memory for a single process P. The high level idea is to
identify and control when pages of this process get evicted from the memory.
Our approach is to hack what pages from the LRU list are selected for eviction (there is a function
page_evictable which is called to decide whether or not to evict a page, we hack here) and make
sure that none of the pages belonging to our prioritized process are selected, unless the upper limit
for memory allocated to the process is reached. This can be known through RSS.

The main function which is called to decide whether or not a page is evictable is page_evictable
from vmscan.c. We place a hook inside this function and return false whenever the particular pagebelongs to our process.
