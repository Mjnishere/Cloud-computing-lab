# Experiment: Hypervisor Performance Analysis

## Objective
Compare the CPU performance of a virtual machine running on:

- **Type-1 Hypervisor:** Proxmox VE
- **Type-2 Hypervisor:** VMware Workstation

The same VM configuration is used on both platforms, and CPU performance is measured using **Sysbench**. :contentReference[oaicite:0]{index=0}

## VM Configuration

| Resource | Configuration |
|---|---|
| OS | Ubuntu |
| CPU | 2 vCPU |
| RAM | 2 GB |
| Disk | 20 GB |
| Benchmark | Sysbench CPU |

## Type-1: Proxmox VE

Create and configure the Ubuntu VM on Proxmox VE with 2 vCPU, 2 GB RAM and 20 GB disk.

Verify the VM using:

```bash
hostnamectl
lscpu
free -h
df -h
