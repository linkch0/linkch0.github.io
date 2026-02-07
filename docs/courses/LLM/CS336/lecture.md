---
icon: fontawesome/solid/chalkboard-user
tags: [Updating]
comments: true
---

# Lectures

```shell
cd trace-viewer
npm run dev
```

## Lecture 1 Overview, tokenization

<http://localhost:5173/?trace=var/traces/lecture_01.json>

![design-decisions](https://s2.loli.net/2025/12/24/L7KqUoAjBalr9w3.webp)

-   **accuracy = efficiency x resources**
-   It's all about efficiency
-   Efficiency drives design decisions

### Basics

Goal: get a basic version of the full pipeline working

Components: tokenization, model architecture, training

**Tokenization**

![tokenized-example](https://s2.loli.net/2025/12/25/m4TaU2NSxdlztV9.webp)

**Architecture**

![transformer-architecture](https://s2.loli.net/2025/12/25/zYeqK8uSEiIOmvB.webp)

---

### Systems

Goal: squeeze the most out of the hardware

Components: kernels, parallelism, inference

**Kernels**

[source](https://miro.medium.com/v2/resize:fit:2000/format:webp/1*6xoBKi5kL2dZpivFe1-zgw.jpeg)

![GPU (A100)](https://s2.loli.net/2025/12/25/A3vsjBcHQGUgZdT.webp)

**Parallelism**

[source](https://www.fibermall.com/blog/wp-content/uploads/2024/09/the-hardware-topology-of-a-typical-8xA100-GPU-host.png)

![multiple GPUs (8 A100s)](https://s2.loli.net/2025/12/25/5FjBgRs17SntNx8.webp)

**Inference**

![prefill-decode](https://s2.loli.net/2025/12/25/y947fhALsi1Q6PK.webp)

---

### Scaling Laws

Goal: do experiments at small scale, predict hyperparameters/loss at large scale

Question: given a FLOPs budget ($C$), use a bigger model ($N$) or train on more tokens ($D$)?

TL;DR: $D^* = 20 N^*$ (e.g., 1.4B parameter model should be trained on 28B tokens)

![chinchilla-isoflop](https://s2.loli.net/2025/12/25/IjJ2qOGoNYl5Z1d.webp)

---

### Data

[source](https://ar5iv.labs.arxiv.org/html/2101.00027/assets/pile_chart2.png)

![pile_chart2](https://s2.loli.net/2025/12/25/7bzaJC2pjNDQM6W.webp)

**Evaluation**

-   Perplexity: textbook evaluation for language models
-   Standardized testing (e.g., MMLU, HellaSwag, GSM8K)
-   Instruction following (e.g., AlpacaEval, IFEval, WildBench)

**Data curation**

**Data processing**

---

### Alignment

**Supervised finetuning (SFT)**

-   Instruction data: (prompt, response) pairs
-   Intuition: base model already has the skills, just need few examples to surface them.  [[Zhou+ 2023\]](https://arxiv.org/pdf/2305.11206.pdf) (1000 examples)
-   Supervised learning: fine-tune model to maximize p(response | prompt).

**Preference data**

-   Data: generate multiple responses using model (e.g., [A, B]) to a given prompt.
-   User provides preferences (e.g., A < B or A > B).

**Verifiers**

-   
    Formal verifiers (e.g., for code, math)
-   Learned verifiers: train against an LM-as-a-judge

**Algorithms**

-   Proximal Policy Optimization (PPO) from reinforcement learning [[Schulman+ 2017\]](https://arxiv.org/pdf/1707.06347.pdf)[[Ouyang+ 2022\]](https://arxiv.org/pdf/2203.02155.pdf)
-   Direct Policy Optimization (DPO): for preference data, simpler [[Rafailov+ 2023\]](https://arxiv.org/pdf/2305.18290.pdf)    
-   Group Relative Preference Optimization (GRPO): remove value function [[Shao+ 2024\]](https://arxiv.org/pdf/2402.03300.pdf)

---

### Tokenization

[Let's build the GPT Tokenizer Andrej Karpath](https://www.youtube.com/watch?v=zduSFxRajkE)

[interactive site](https://tiktokenizer.vercel.app)

![image-20251226162356817](../../../../../../Library/Application%20Support/typora-user-images/image-20251226162356817.png)

-   `hello` and `\space hello` is different token, space is a part of token
-   The numbers are chopped from left to right.

1.   **Character-based tokenization**

     ```python
     assert ord("a") == 97
     assert ord("🌍") == 127757
     assert chr(97) == "a"
     assert chr(127757) == "🌍"
     ```

     -   **Problem: Large and Sparse**
     -   Problem 1: this is a very large vocabulary. There are approximately 150K Unicode characters.  [[Wikipedia\]](https://en.wikipedia.org/wiki/List_of_Unicode_characters)
     -   Problem 2: many characters are quite rare (e.g., 🌍), which is inefficient use of the vocabulary. Many sparsity.

2.   **Byte-based tokenization**

     ```python
     assert bytes("a", encoding="utf-8") == b"a"
     assert bytes("🌍", encoding="utf-8") == b"\xf0\x9f\x8c\x8d"
     ```

     -   **Problem: Long sequences. Compression ratio is 1.**
     -   Unicode strings can be represented as a sequence of bytes, which can be represented by integers between 0 and 255. The most common Unicode encoding is  [UTF-8](https://en.wikipedia.org/wiki/UTF-8)
     -   The compression ratio is terrible, which means the sequences will be too long.

3.   **Word-based tokenization**

     ```python
     GPT2_TOKENIZER_REGEX = \
         r"""'(?:[sdmt]|ll|ve|re)| ?\p{L}+| ?\p{N}+| ?[^\s\p{L}\p{N}]+|\s+(?!\S)|\s+"""
     ```

     -   **Problem: Unfixed vocabulary size.  UNK token.**
     -   Use regular expression to split strings into words
     -   New words we haven't seen during training get a special UNK token, which is ugly and can mess up perplexity calculations.

4.   **Byte Pair Encoding (BPE)**

     -   Basic idea: *train* the tokenizer on raw text to automatically determine the vocabulary
     -   Intuition: common sequences of characters are represented by a single token, rare sequences are represented by many tokens.
     -   Sketch: start with each byte as a token, and successively merge the most common pair of adjacent tokens.
     
     <img src="https://s2.loli.net/2026/01/14/NRheUdmoC7rsp4T.webp" alt="image-20260114161845791" style="zoom: 33%;" />
     
     <img src="https://s2.loli.net/2026/01/14/LSWptVrFN9AavK1.webp" alt="image-20260114161927363" style="zoom:33%;" />

## Lecture 2 PyTorch, resource accounting

<http://localhost:5173/?trace=var/traces/lecture_02.json>
