---
title: "Hector-V: A Heterogeneous CPU Architecture for Secure RISC-V Execution Environment"
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

# Background

## Existing TEEs

- Virtual Processor Based: Intel SGX, Arm Trustzone

### Pros and Cons

- Pros: high performance, no additional hardware
- Cons: cache/transient side channel attacks, no I/O protection

---

- External Co-Processor Based: Google Titan, Samsung eSE

### Pros and Cons

- Pros: cache/transient side channel attacks mitigated
- Cons: a communication interface required (which is typically slow and vulnerable to physical probing/sniffing attacks), addtional hardware required

---

- On-SoC Processor Based: Apple's SEP, Microsoft's Pluton, and HECTOR-V

### Pros and Cons

- Pros: fast secure commnunication channels, probing and sniffing attacks mitigated, cache/transient side channel mitigated
- Cons: additional hardware required

---

# HECTOR-V Design

## Threat Model

- a combination of bugs in kernel exists
- missing state-of-the-art protection strategies (ASLR, etc)
- bugs exist in the trustlets (can be exploited through the REE/TEE channel)
- cache/transient based side channel attacks
- malicious trustlets
- ...

### Summary
Assuming a powerful attacker having full control over user app, OS, turstlets or even hypervisor running on the application processor.

## Goals

- Secure I/O
- Control-flow Integrity

To guarantee this two goals, a TEE is proposed with two key parts: a basic HECTOR-V and a RVSCP (RISCV Secure Co-Processor) extension (we will mainly discuss the extended architecture with both parts)

## Design

![overall](overall.png)

---

![detailed](detailed.png)

---

## HECTOR-V

- Peripheral Wrapper

Peripheral examples: SD-card controller, BRAM, UART, ...

The wrapper is designed for the security monitor to manage accesses to the peripherals.

- Security Monitor

The security monitor contains a table to manage peripherals.

- Security Monitor Owner

The entity that can configure the security monitor. The ownership can be transferred between the application processors and RVSCP virtualized processors.

- Interconnect

Use AMBA AXI4 and AXI4-lite protocols for communication between components of HECTOR-V. AXI4 is for data tranferring and AXI4-lite for configuration.

--- 

## How do the Trusted I/O Paths work?

### Identifier
The identifier consists of three parts:
- Core ID (1 bit)
- Process ID (4 bits)
- Peripheral ID (10 bits) 

Before accessing to a peripheral, the peripheral wrapper will check the ID of the request. The request is blocked if the ID does not match.

The Core ID is determined via hardware, which cannot be changed by softwares. The other two can be assigned by the security monitor.

- How is ID transferred?

Using the user-defined signal in the AXI4 protocol (1024-bit long), there is no protocol overhead.

---

### Security Monitor
The security monitor maintains a table for peripheral management.

Supported commands:

- Claim
- Release
- Withdraw
- Transfer

---

- Claim

1. send a claim request to the security monitor
2. the security monitor checks whether the peripheral is unclaimed
	- unclaimed: check whether the requester is in the list of IDs that are permitted to access the peripheral. If not permitted, the request fails.
	- claimed: the security monitor notifies the requester. The requester needs to wait until the peripheral is released.

---

- Release









