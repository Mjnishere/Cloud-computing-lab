# Performance Analysis of Type-1 and Type-2 Hypervisors

This repository contains the configuration details, execution steps, and observation templates for comparing the CPU performance of a Type-1 hypervisor (Proxmox VE) and a Type-2 hypervisor (VMware Workstation). 

For comprehensive step-by-step laboratory instructions, refer to the official documentation provided in the file named Lab-Manual-Hypervisor-Performance-Analysis.docx.

## Objective
To create identically configured virtual machines (VMs) on both Proxmox VE and VMware Workstation and measure their respective CPU performance using the Sysbench benchmarking tool.

## Virtual Machine Specifications
Both virtual machines are provisioned with identical hardware allocations to ensure an accurate performance comparison.

| Resource | Allocation |
| :--- | :--- |
| **Guest Operating System** | Ubuntu Linux (64-bit) |
| **Virtual CPUs (vCPU)** | 2 (1 Socket, 2 Cores) |
| **Memory (RAM)** | 2048 MB (2 GB) |
| **Virtual Disk Size** | 20 GB |
| **Network Configuration** | vmbr0 (Proxmox) / NAT (VMware) |

## Part A: Proxmox VE (Type-1 Hypervisor) Setup
Proxmox VE is deployed on a centralized bare-metal server and accessed via its web-based management interface.

### 1. VM Creation
1. Access the Proxmox VE interface at `https://<PROXMOX_SERVER_IP>:8006`.
2. Authenticate using the provided credentials.
3. Select the Proxmox server node under the `Datacenter` hierarchy and click **Create VM**.
4. Follow the creation wizard using the recommended naming convention: `<Name>-Type1` (e.g., `CC-Experiment1-Type1`).
5. Attach the Ubuntu ISO (e.g., `ubuntu-22.04.iso`) from the local storage.
6. Allocate 20 GB on `local-lvm`, 2 Cores, 2048 MiB Memory, and the `vmbr0` network bridge.
7. Confirm settings, start the VM, open the Console, and complete the Ubuntu installation process.

## Part B: VMware Workstation (Type-2 Hypervisor) Setup
VMware Workstation runs as an application on top of a host operating system.

### 1. VM Creation
1. Launch VMware Workstation and select **Create a New Virtual Machine** using the Typical (recommended) configuration.
2. Browse and select the Ubuntu ISO file.
3. Use the recommended naming convention: `CC-Experiment1-Type2`.
4. Set the maximum disk size to 20 GB and store the virtual disk as a single file.
5. Click **Customize Hardware** to adjust the resources.
6. Allocate 2048 MB of Memory and 2 Processors (1 socket, 2 cores per processor).
7. Ensure the Network Adapter is set to NAT.
8. Finish the setup, power on the virtual machine, and install Ubuntu.

## Benchmarking Methodology
Once the Ubuntu installation is complete on both hypervisors, the following diagnostic and benchmarking procedures must be executed within the terminal of each virtual machine.

### 1. System Verification
Verify the hardware allocation using the following commands:

    hostnamectl      # Verify OS and Kernel details
    lscpu            # Analyze CPU configuration and virtualization type
    free -h          # Analyze Memory allocation
    df -h            # Analyze Disk capacity
    top              # Monitor live system resource utilization

### 2. Installing Sysbench
Sysbench is utilized to perform the CPU performance analysis.

    sudo apt update
    sudo apt install sysbench -y
    sysbench --version

### 3. Executing the Benchmark
Run the following command on both the Type-1 and Type-2 VMs to execute the CPU benchmark:

    sysbench cpu --cpu-max-prime=20000 run

## Observation and Results
After running the Sysbench CPU test, record the performance statistics (Total execution time, Total events, Events per second, and Latency statistics) in the tables below for comparison.

### Type-1 Hypervisor Performance (Proxmox VE)
| Parameter | Observation |
| :--- | :--- |
| **Hypervisor** | Proxmox VE |
| **Hypervisor Type** | Type-1 |
| **Total Execution Time** | |
| **Total Events** | |
| **Events per Second** | |
| **Average Latency** | |

### Type-2 Hypervisor Performance (VMware Workstation)
| Parameter | Observation |
| :--- | :--- |
| **Hypervisor** | VMware Workstation |
| **Hypervisor Type** | Type-2 |
| **Total Execution Time** | |
| **Total Events** | |
| **Events per Second** | |
| **Minimum Latency** | |
| **Average Latency** | |
| **Maximum Latency** | |

## Shutdown Procedure
Upon completing the benchmarking and recording the results, ensure the virtual machines are properly powered down:

    sudo poweroff

Alternatively, utilize the respective hypervisor management interfaces to shut down the guest operating systems.
