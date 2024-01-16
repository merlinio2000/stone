
references [[Modules#IMPORT / EXPORT in ARM]]


# Object Files

**ACCORDING TO ELF** (Executable and Linkable Format)

contains all compiled data of a module

Sections:
- Code
	- code and const data of the module
	- base addr at `0x0`
- Data
	- all global variables of the module
	- base addr at `0x0`
- Symbol table
	- all symbols + their attributes (global/local, reference, etc)
- Relocation table
	- which bytes of the data and code section need to be adjusted after merging the sections during linking?

## From ASM symbols to object file symbols


![[asm_to_obj_sym_basics.png]]

### References
- **imported** symbols in asm code -> global **reference** symbols in object file

### Global
- **exported** symbols in asm code -> global symbols in object file

### Local
- **internal** symbols in asm code -> **local** symbols in object file

![[c_to_obj_sym.png]]


#### Example object file

![[elf_obj_ex_square.png]]

![[elf_obj_ex_main1.png]]
![[elf_obj_ex_main2.png]]
![[elf_obj_ex_main3.png]]


# Executable File

`.axf` = ARM eXecutbale File

Contains all **linked** data of the program

Sections:
- Code
	- code and const data of the program
- Data
	- all global variables of the program
- Symbol table
	- all symbols with attributes (global/local, etc.)

**May** still contain unresolved symbols for linking with **shared** (dynamic) libraries



# Linker

- merges code sections
	- (simplified: concatenates code together into one big code section)
- merges data sections
- symbol resolution (refs to other modules)
- address relocation
	- references have to be updated to the new position
		of the symbols
- In: [[#Object Files]]
- out: [[#Executable File]]


![[linker_basics.png]]




## Resolution

![[resolution_ex.png]]

![[resolution_ex_elf.png]]




## Relocation

![[relocation_ex_addr.png]]
![[relocation_ex_symbols.png]]