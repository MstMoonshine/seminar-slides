---
title: "HECTOR-V"
author: "Mingde Ren"
institute: "COMPASS"
urlcolor: blue
colortheme: "beaver"
date: "March 9, 2021"
theme: "Heverlee"
aspectratio: 169
lang: en-US
marp: true
---

# Hector-V: A Heterogeneous CPU Architecture for Secure RISC-V Execution Environment


---

# Background


## Existing TEEs

- Virtual Processor Based: Intel SGX, Arm Trustzone

### Pros and Cons

- Pros: high performance, no additional hardware
- Cons: cache/transient attacks, no I/O protection