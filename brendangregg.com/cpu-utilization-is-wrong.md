# cpu-utilization-is-wrong

- CPU utilization % is NOT a measure of how "busy" a CPU is. It can include stalled work and measures non-idle time, not active-use time

- Use `perf stat -a -- sleep 10` to measure performance across a system
    - key metric is `instructions per cycle` aka `insns per cycle`
        - shows on average how many instructions were completed for each cpu clock cycle
        - if IPC is < 1.0 you are likely memory-stalled
        - if IPC is > 1.0 you are likely instruction bound.
        - For my above rules, I split on an IPC of 1.0. Where did I get that from? I made it up, based on my prior work with PMCs. Here's how you can get a value that's custom for your system and runtime: write two dummy workloads, one that is CPU bound, and one memory bound. Measure their IPC, then calculate their mid point.
    - if in the cloud you may not have access to PMCs

<RESEARCH ME> http://www.brendangregg.com/blog/2017-05-04/the-pmcs-of-ec2.html