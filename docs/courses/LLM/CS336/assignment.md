---
icon: fontawesome/solid/pen
comments: true
hide:
  - navigation
tags: [Updating]
---

# Assignments

## Assignment 1 Basics

[Code](https://github.com/stanford-cs336/assignment1-basics), [PDF](https://github.com/stanford-cs336/assignment1-basics/blob/main/cs336_spring2025_assignment1_basics.pdf), [Leaderboard](https://github.com/stanford-cs336/spring2025-assignment1-basics-leaderboard/tree/master)

-   Implement BPE tokenizer

-   Implement Transformer, cross-entropy loss, AdamW optimizer, training loop

-   Train on TinyStories and OpenWebText

-   Leaderboard: minimize OpenWebText perplexity given 90 minutes on a H100 

---

## Assignment 2 Systems

[Code](https://github.com/stanford-cs336/assignment2-systems), [PDF](https://github.com/stanford-cs336/assignment2-systems/blob/main/cs336_spring2025_assignment2_systems.pdf), [Leaderboard](https://github.com/stanford-cs336/assignment2-systems-leaderboard/tree/main)

-   Implement a fused RMSNorm kernel in Triton
-   Implement distributed data parallel training
-   Implement optimizer state sharding

Benchmark and profile the implementations

---

## Assignment 3 Scaling

[Code](https://github.com/stanford-cs336/assignment3-scaling), [PDF](https://github.com/stanford-cs336/assignment3-scaling/blob/main/cs336_spring2025_assignment3_scaling.pdf)

-   We define a training API (hyperparameters -> loss) based on previous runs
-   Submit "training jobs" (under a FLOPs budget) and gather data points
-   Fit a scaling law to the data points
-   Submit predictions for scaled up hyperparameters
-   Leaderboard: minimize loss given FLOPs budget

---

## Assignment 4 Data

[Code](https://github.com/stanford-cs336/assignment4-data), [PDF](https://github.com/stanford-cs336/assignment4-data/blob/main/cs336_spring2025_assignment4_data.pdf), [Leaderboard](https://github.com/stanford-cs336/assignment4-data-leaderboard)

-   Convert Common Crawl HTML to text
-   Train classifiers to filter for quality and harmful content
-   Deduplication using MinHash
-   Leaderboard: minimize perplexity given token budget

---

## Assignment 5 Alignment

[Code](https://github.com/stanford-cs336/assignment5-alignment), [PDF](https://github.com/stanford-cs336/assignment5-alignment/blob/master/cs336_spring2025_assignment5_alignment.pdf)

-   Implement supervised fine-tuning   
-   Implement Direct Preference Optimization (DPO)
-   Implement Group Relative Preference Optimization (GRPO)
