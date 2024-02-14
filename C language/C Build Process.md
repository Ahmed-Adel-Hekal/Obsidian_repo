
c build process consist of 3 phases :
1- Compiling     2-Linking           3- Loading 

---
1- ***Compiling***
consist of :  1-Front end processing 
		   2-Middle end processing
		   3-Backend process

1.1 ***Front end processing***
1.1.1 -Pre-processing :
* The pre-processor evaluate the preprocessor directive and perfrom text replacement 
* the  input to the preprocessor is known as preprocessed translation unit,and output is a post processed translation unit.
1.1.2 -white-space removal : 
	- c ignores whitespace so the first stage of pre-processing the translation unit is to strip out all whitespace.
1.1.3 - Tokenising :
	 - in this stage,the program is converted to stream of tokens. a token can be a keyword , an operator , an identifier 
1.1.4 -Syntax Analysis :
	 - Ensures that tokens are organized in the correct way, according to the c role 
	 - if not, the compiler will produce an error
	 - the output of this stage is called "Parse Tree"
	 - a parse tree detect associativity and precedence of operator.
1.1.5 - Intermidiate representation : 
	 - Transform the parse tree to sime known machine independent  from known as an "intermediate representation"
	- this allow compiler vendor to support multiple languages
	- In gcc , Ir are typically in the form of an abstraction syntax tree (ast) or pseudo-code
1.2- **Middle-End Processing**
	1.2.1 Semantic Analysis:
		 - check logical structure of the program
		 - problems found at this stage will produce "warning"
		 - At this stage symbol table is constructed and any debug information will be produced
	 1.2.2 Optimization 
		 - transform the code into functional - euivalent but smaller or faster 
		 - Optimization process includes : 
			 - Inline expansion of functiion
			 - dead code removal 
			 - loop unrolling 
			 - register allocation 
1.3.1 Backend Processing :
- Memory Allocation 
- Exports Table 
- - Exports section contains global symbols either functions or variables.
- Import tables
- - Imports section contains symbol names that are needed from other object files.
- Exports, imports, and symbol table sections are used by the linker during linking stage.
----
2- ***Linking***
- Symbol Resolution: 
	- resolve refrence between object files
	- unresolved refrence are searched for in all specified libraries. if after this the linker cannot reolve a symbol it generates an "unresolved symbol" error
	- if the linker finds the same symbol defuned in two object files, it will report a "redfinition error"
- Section concatenation 
		- the linker concatenates like-named sections from the input object files.
		- program addresses are adjusted to take account of the concatenation
- Section allocation 
	- each section is given an absolute address in memory 
	- sections are concatenated for some base address
- Data Initialization 
	- Any initialized data must be stored in non-volatile memory 
	- on startup any non-const data must be copied to ram and read-only sections like code are also copied to ram to speedup execution
	- the linker creates extra section to enable copying from rom to ram . each section is divided into 2 parts one for the rom (shadow data) and one for the ram (runtime location)
	- .bss section has no shadow section. it is initialized as part of the startup code
- ***LINKER CONTROL***
	- linker can be controled via linker control file (LCF)or command line 
	- LCF defines physical memory layout (Flash| sRam) and placement of the diffrent prog region . 
	- LCF syntax is compiler dependent 
	- LCF specify the size and location of the the stack and heap
	- the linker will perform check to ensure that code and data sections will fit into the designated regions of memory.
	- the output of the locating process is a load file in a platform independent format , commonly .Elf or .DWARF
- 3 ***LOADING***
		-convert elf or Dwarf file into .bin or hex