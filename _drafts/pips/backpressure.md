name: backpressure
topic:
author:
tags: [[cs_learning]]
link: https://medium.com/@jayphelps/backpressure-explained-the-flow-of-data-through-software-2350b3e77ce7

-   **Control** the producer (slow down/speed up is decided by consumer)
-   **Buffer** (accumulate incoming data spikes temporarily) - unbounded buffers are a common source of memory crashes in servers
-   **Drop** (sample a percentage of the incoming data) - sampling
-   Ignore

code paradigms for backpressure
- pull - pull based server the consumer controls the producer - nodejs streams
- push the producer is in control - rxjs