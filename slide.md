---
title: "Summary for Last Week"
author: "Haonan Lu, Wenxuan Shi, Xueying Zhang"
institute: "COMPASS"
urlcolor: blue
colortheme: "beaver"
date: "March 9, 2021"
theme: "Heverlee"
aspectratio: 169
lang: en-US
marp: true
---

# iing

## Last Week's work

Read a paper " iReplayer: In-situ and Identical Record-and-Replay for Multithread Applications ".

---

## Features

- in-situ replay: in the same process
- identical replay: strictly preserves all system states, results of system calls, the order and results of synchronizations, and the same memory allocations/deallocations
- high efficiency: 3% recording overhead

---

## Overview

- Divide the entire execution into several epochs, based on irrevocable system calls, abnormal exits and user-defined criteria, and always replay the last-epoch. 
- When a thread encounters the end of one epoch, it will coordinate with other threads to pause the execution. And then choose to roll-back or not. 
- Record: the order of synchronization and system calls in the same thread and across multiple threads with a special data structure

---

## Identical replay

- Race of memory access: try many times
- System call: make delicate classification. Repeatable, recordable, revocable(files), deferrable(delay) and irrevocable. 
- Per-thread heap and a super heap (from other articles). 

---

## conclusion

Not very useful for us. The key point of this article concentrates on how to record and how to synchronize multi-threading, which we don’t need to take into account.

---

## Next week’s plan

Take a TOFEL test

