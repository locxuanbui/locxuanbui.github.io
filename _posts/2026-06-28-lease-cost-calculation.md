---
title: "A Julia package to calculate cost of a lease"
---

I've recently shopped for a new car lease, and felt the need of a tool to calculate the cost of every lease option that the dealer presented to me. So I wrote [LeaseCalc.jl](https://github.com/locxuanbui/LeaseCalc.jl), which is a Julia tool to calculate the total and per-year costs, with and without taking into account inflation.

Here is an example usage to calculate the cost of a (\\$4000 down payment, \\$300 per month, 36 months) lease:
```
using LeaseCalc

leasecost(4000, 300, 36)

# Output:
# Total: 14800
# Cost per year: 4933.333333333333
# Total (inflation discounted): 14166.130631800457
# Cost per year (inflation discounted): 4722.043543933485
```

I hardcoded the inflation discount factor as 0.35% per month (roughly 4% per year). Then, the total inflation discounted cost is:

$$
C_{total} = C_{down} + \sum_{i=1}^N \frac{c_m}{(1 + \alpha)^{i-1}}\,,
$$

where $C_{down}$ is the down payment cost, $c_m$ is the (fixed) monthly cost, $N$ is the number of months in the lease, and $\alpha = 0.0035$ is the inflation discount factor.
