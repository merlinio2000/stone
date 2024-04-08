
# Lifecycle

Each process is in one of three states.

- Running
	CPU Assigned
- Ready
	Waiting for first go or temporarily stopped (idle)
- Blocked
	Dependencies not met for running
	 - resource unavailable
	 - waiting for interrupt
	 - sleeping
	 - job control
![[proc_lifecycle.png]]


### Termination

A program returns:
- Voluntary (return from main)
- Involuntary exit (seg fault / div by zero)
- Murder, killed by request (SIGKILL)



# Mode Switch vs Context Switch

Mode switch: from process to Interrupt (e.g. Syscalls)
Context switch: scheduler re-assigns CPU to other process

![[proc_modeSwitch-vs-ctxSwitch.png]]




# Process Control Block (PCB)

Persists state of each process, allows Context Switch
![[proc_pcb.png]]

The **process table** is (on Linux) a doubly-linked list of these PCB's
