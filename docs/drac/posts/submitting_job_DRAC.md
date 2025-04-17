---
date: 2025-04-17
description: Submitting job
categories:
  - DRAC
authors:
  - saeidamiri1
---

# Submitting job
 Please do not run any computations on the login node. The login node resource (RAM\CPU) is intended ONLY for tasks such as editing scripts and downloading\transferring data.
To learn how to properly submit jobs, please refer to the following guide:
[Digital Research Alliance of Canada](https://docs.alliancecan.ca/wiki/Running_jobs). 
Using the login node for computations can result in a warning from DRAC, and repeated violations lead to account suspension.


## Optimal CPU\RAM
Since we are using shared resources, please avoid submitting too many jobs  using excessive RAM/CPU (if your  job requested  30 GB RAM and only used 10 GB, DRAC adds 20 GB as wasted resources to your account :disappointed: ). And DRAC may hold your jobs in the pending state if your resource wasted usage is too high.
If you notice your jobs are pending for a long time longer than normal on Beluga (our main resource), consider canceling them and resubmitting on other DRAC resources like Narval or Cedar.

If you're writing code in Python or R, run your code in multithreaded mode to improve performance and utilize all available CPU and RAM resources.
I often use the command "seff JOBID" to check how much RAM and CPU my job used. This helps me request the appropriate resources for future runs. Many pipelines support multithreading, so make sure to enable it to fully utilize the available resources.
When I'm unsure about a pipeline's resource usage, I usually run a small test job first to estimate the RAM usage. Based on that, I adjust the resource requests accordingly.
Requesting 4 CPUs and 16 GB of RAM is typically optimal, and Beluga usually allocates these resources quickly. However, if you request 16 GB of RAM for 4 days and your job only uses 20% of it, you're effectively wasting 80% of the allocated resources.
Don’t worry if your job runs for only a short time—that’s perfectly fine. The real concern is when you submit many jobs at once, each reserving resources for several days. If those jobs end up wasting a large amount of CPU or RAM, DRAC may deprioritize your future jobs due to inefficient resource usage.
