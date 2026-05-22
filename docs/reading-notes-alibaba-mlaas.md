# Key Findings
- We can predict the workload of a data center (GPU and CPU usages) that is required for the capacity planning model. Using the historical completion times, it is possible to estimate workloads per "data center - gpu/cpu type - date (or some date range)"
- Planning should take the GPU type granulariy into consideration in order to generate meaningful plans.
- Sharing can be assumed at planner granularity; contention effects are a runtime concern.


# Skeptical
- The paper highlights GPU sharing as their core contribution, however in today's world it is now a widely used practice, so not sure how useful this information for our project.
- Their characterization is Alibaba 2020, and the question is whether the patterns (over-request gap, duration distribution, weekday pattern) still hold for 2026 European workloads.

# Open Question
- In the system's current configuration, are there any capacity mismatch? The paper only focuses on the existing setting and doesn't discuss any over or under capacity problems.