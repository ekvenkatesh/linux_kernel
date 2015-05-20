# linux_kernel
Pet projects on linux kernel

Memory Allocation based on Process Priority
===========================================
The aim of this project is to control the amount of physical memory allocated to a process according
to its priority. The notion of priority of a process is already used in CPU and IO scheduling to
decide how much of the resource (i.e., time) the process is allowed to use. I extend this notion onto
physical memory allocation.

When the system is operating on low load, processes get as much memory as needed. However,
when there are multiple processes competing for memory, pages have to be swapped in and out of
the physical memory. This affects the performance of the process. In such a scenario, I allow a
particular process (set of processes) which is (are) considered “high priority” to retain all their
pages without any pages getting swapped out. This will boost the performance of that process
(obviously, at the cost of another less priority process).

The futuristic goal of this project is to have a mode based operation of the kernel. Applications are
categorized as belonging to one mode amongst a set of modes (gaming, entertainment, work etc.).
Depending on the selected mode, the particular set of applications is given prioritized access to
resources.

For example, when I want to study, I will set the mode to “work”. The OS will automatically
prioritize work related applications (which will be specified by me apriori, like, Browser, Eclipse
IDE, LibreOffice Writer etc). Even if a batch application is running in the background (such as the
download of a movie which I want to watch later), that application will be deprioritized. 
