
A collection of [[Process]]es (tasks) bound to a set of resource limits or parameters

- defined in the [[#cgroup filesystem]]


##### cgroup filesystem

(both v1 and v2)
used to communicate with the linux kernel about resource control
(structured alternative to just variables in memory)

- purely virtual, exists only in RAM (`tmpfs`)
- similar to `/proc`

Hierarchically structured, see e.g. `tree /sys/fs/cgroup/pids`


# cgroups V1

Each v1 controller **may** be in a separate filesystem
All controllers can be co-mounted to a single filesystem

**control groups** are represented by directories, sub control groups as sub-directories

A task can **not** be a member of different cgroups in the same hierarchy

#### tasks (threads) vs processes

**DONT** do this, dangerous (e.g. address space is shared so separate limits make no sense)
Processes and task are treated differently, in v1 it is possible to manipulate the cgroup
membership of every thread of a process



## cgroup contoller mounting

Individual controllers can be mounted at any location
Example: mount `cpu` controller: 
```sh
mount -t cgroup -o cpu none /sys/fs/cgroup/cpu
```

**THE CPU controller can now not be mounted against a different hierarchy**, however 