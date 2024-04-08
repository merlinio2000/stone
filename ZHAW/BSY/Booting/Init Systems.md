
Act as the root process (PID=1) of the process tree

### init

- simply runs shell scripts from /etc/rc
- then getty on terminals controlled trhough /etc/ttys
- NO [[#Run Levels]]


## SysV init

- at ANY moment, system is in a predetermined state -> [[#Run Levels]]
- inter-service dependencies are coded in the launch scripts
	- (e.g. sshd requires network daemon)

### Run Levels
![[init_runLevels.png]]


# systemd
- mostly backwards compatible with [[#System V]]
- declared through custom `.service` files
- coordinated parallel startup of services
- manages the "system" not "just" services

The systemd **User-Instance** (`--user` flag)

## Units 

Entities are called **Units**

These **units** encapsulate **Objects**
	services, mounts, devices, timers

Units are in one of these states:
- active
- inactive
- activating/deactivating
- failed

One unit might depend on another unit in a certain state

![[init_systemd_units.png]]


### Service Units

describe birth-to-death how to manage a running service/application

includes
- start/stop commands
- dependencies
- automatic start/stop/restart conditions


### Target Units

DO-NOT provide any functionality

Serve to **group** other [[#Units]] via dependencies
- useful as boot targets
- establish standardized names for synchronisation points
	(cumulative state that represent a coordinated total of a set 
		of system service states)
- allow to "pull" the system into a state
- on boot: systemd activates `default.target`
		(activates all on-boot services by pulling them as 
			dependencies)