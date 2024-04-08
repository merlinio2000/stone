

Lightweight sub-units of [[Process]]

Adressspace is shared with parent process

Each thread has its own:
- Program Counter (which instruction comes next)
- registers
- stack (reside in stack of owning process)




# Threads in Linux

Threads are also [[Process]]es (**Tasks**) in Linux

Tasks in Linux share a configurable set of resources (address space, file descr., sockets, sighandlers, etc..)
So Threads are simply implemented as a Task that shares everything with the process creating those threads
