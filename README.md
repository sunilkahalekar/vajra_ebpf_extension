# Vajra osquery Extension for Linux 

OSQuery Extension wtih eBPF extends the core osquery on Linux by adding real time event collection capabilities to osquery on Linux platform. The capabilities are built using the kernel services of linux. It is a step in the direction aimed at increasing osquery footprint and adoption on linux platform. With the extension acting as a proxy into linux kernel for osquery, the possibilities can be enormous. The extension supports the kernal versions from 4.16 or onwards.

# What it does: 

The extension bridges the feature gap of osquery on Linux in comparison to auditd adding the following into the osquery: 
1. Granular File Integrity Monitoring (FIM) 
2. Process Auditing 
3. Socket (listen, accept, connect and close) events 
4. Ability to query the current status of security products installed on the system 
5. Ability to monitor application specific log files


It uses new kernel functionality (eBPF) to capture the process, socket, and other types of events.
With eBPF enabled we will have access to tables bpf_process_events, bpf_file_events and bpf_socket_events that are equivalent to the standard process_events and socket_events tables.

Enabling eBPF for osquery on Linux requires the following flags:

------------------------------------------------------
  --disable_events=false --enable_bpf_events=true
---

Event list 
/event/list
Request type: GET
Parameters: filter Value: JSON containing at least one field from [host_identifier, is_open, start_time, end_time]
Response: List of all events filtered using filter (where host id == host_identifier AND, isopen = is_open, AND event time >= start_time AND event time <= end_time)
boolean value can be given as true/t 

host_identifier| is_open | event_time

	 --disable_events=false --enable_bpf_events=true
Container Monitoring
A further advantage when using eBPF rather than the audit subsystem is greater visibility into containers and management systems including both Docker and Kubernetes.
