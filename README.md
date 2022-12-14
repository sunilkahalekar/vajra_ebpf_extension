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

Performance: We can get those system calls that are attach to kernel trace points, attach to user space function calls and all of this has potential to be dynamically configured at osquery runtime and because these programs run within the kernel while making less of a performance impact on the systems.

Security: From a security space just some high level ideas interested in all syscalls of interest, relevant for our security use cases, track the signals being sent to processes, kernel modules being loaded and unloaded. Along with that which functions are being executed, when externally linked functions are called in a binary. This is like one of the persistence techniques for linux that you’d find on the MITRE ATT&CK framework. We want to hook into the functions from our mysql server and start inspecting those and this will help to track down bugs and production and performance wins for the whole organization.

Resource Consumption: We can see a lot of examples using bpf to measure all sorts of data points of interest such as the latency and the resource consumption of the network, our file system or any kind of I/O within the system, can count and measure the functions within user space programs.

Use cases: In future, look at the data they’re collecting and think about what of this would map. This is useful for aggregating and shipping that information from the hosts into our logging pipelines or maybe making it available via live query. Really think, how the new data might be enhanced by the abstractions that we’ve built in osquery. So, audit and ebpf are both viable approaches for doing this kind of low-level instrumentation on linux. Users need to consider some various points when deciding which to use and you know some of these would be like the support that your kernel has the workloads that you’re running on your system. It could be reasonable that a mix of the two approaches is what you use within your organization because you have a wide range of kernels deployed and you have a wide range of workloads and in some places you’ll use one and some places the other.

Alongwith osquery, eBPF has potentially increases the observability. It can start replacing some of the functionality that’s there but there is a whole world of more that we can do with this information so being closer to the kernel running. These programs within the kernel means we can record more data with a lower performance cost so we can take advantage of that to get at things that we never thought were possible before.
