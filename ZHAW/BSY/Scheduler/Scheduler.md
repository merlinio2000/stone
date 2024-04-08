# FIFO 
(aka First Come First Served FCFS)

run to completion then next


# Round-Robin

Give each active task a **Quantum** of time, after that give a **quantum** to the next, etc...


# Fair Scheduling

Try to treat each task equal, but some tasks are more equal than others so they might be allowed to take up more



# Real Time


## Rate Monotonic

Every task runs with a deadline before it has to yield for other processes (priority based)


## Earliest Deadline First

Which task has the earliest deadline(based on priority)? Dispatch that one




# Linux Scheduling

One single task queue
Different tasks use different schedulers on same machine

Task can cooperate using `yield`

Tasks can be **pinned** to a specific core (other tasks might still execute on that core)

### Real-Time Policy

- SCHED_DEADLINE [[#Earliest Deadline First]]
	- Highest Priority
	- ! NOT ALLOWED TO FORK
	- CBS(Constant Bandwidth Server) allocates sporadic tasks
- SCHED_FIFO [[#FIFO]]
	- Higher PRIO than [[#Round-Robin]]
- SCHED_RR [[#Round-Robin]]


### Normal Policy

- SCHED_OTHER
	- CFS Queue(completely fair scheduler) (using Read-Black tree)
	- `nice` determines position in tree (virtual clock runs faster for more nice)
- SCHED_BATCH
- SCHED_IDLE



## Priorities


High-to-low

! `top` might show lower priorities as negative numbers

#### Real-Time Policy

**Priority means order of execution**

Since user needs to be able to regain control of the machine 
-> configurable % of CPU time can be assigned to NON RT tasks
#### Normal Policy

**nice**-ness determines time assigned to task
Execution order determined by algorithm