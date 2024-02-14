

- gcc -E file.c -o file.i  ----> preprocessor only 
- gcc -s file.c -o out.asm   ----> only till compiler 
- gcc -c file.c -o file.out ---> stop after assemble
- objdump.exe -lsd file.elf --> to disassemble object file
- 