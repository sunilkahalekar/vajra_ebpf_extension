# Vajra osquery Extension for Linux 

OSQuery Extension wtih eBPF extends the core osquery on Linux by adding real time event collection capabilities to osquery on Linux platform. The capabilities are built using the kernel services of linux. It is a step in the direction aimed at increasing osquery footprint and adoption on linux platform. With the extension acting as a proxy into linux kernel for osquery, the possibilities can be enormous. The extension supports the kernal versions from 4.16 or onwards.

# What it does: 

The extension bridges the feature gap of osquery on Linux in comparison to auditd adding the following into the osquery: 
1. Granular File Integrity Monitoring (FIM) 
2. Process Auditing 
3. Socket events (listen, accept, connect and close) give information like protocol,local_address, remote_address, local_port and remote_port
4. Ability to monitor application specific log files


It uses new kernel functionality (eBPF) to capture the process, file and socket events.
With eBPF enabled we will have access to tables bpf_process_events, bpf_file_events and bpf_socket_events that are equivalent to the standard process_events, file_event and socket_events tables.

Enabling eBPF for osquery on Linux requires the following flags:


	 --disable_events=false --enable_bpf_events=true

# Container Monitoring
A further advantage when using eBPF rather than the audit subsystem is greater visibility into containers and management systems including both Docker and Kubernetes.


# eBPF Features

## Performance: 
We can get those system calls that are attach to kernel trace points, attach to user space function calls and all of this has potential to be dynamically configured at osquery runtime and because these programs run within the kernel while making less of a performance impact on the systems.

## Security: 
From a security space just some high level ideas interested in all syscalls of interest, relevant for our security use cases, track the signals being sent to processes, kernel modules being loaded and unloaded. Along with that which functions are being executed, when externally linked functions are called in a binary. This is like one of the persistence techniques for linux that you’d find on the MITRE ATT&CK framework. We want to hook into the functions from our mysql server and start inspecting those and this will help to track down bugs and production and performance wins for the whole organization.

## Resource Consumption: 
We can see a lot of examples using bpf to measure all sorts of data points of interest such as the latency and the resource consumption of the network, our file system or any kind of I/O within the system, can count and measure the functions within user space programs.


Alongwith osquery, eBPF has potentially increases the observability. These programs within the kernel means we can record more data with a lower performance cost so we can take advantage of that to get at things that we never thought were possible before.
