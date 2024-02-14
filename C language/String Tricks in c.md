

```c
#include <stdio.h>

int main() {
    char c;
    char s[100];
    char ss[100];

    scanf("%c", &c);
    scanf("%s", s);  // No need to use &s, s is already an array
    scanf("\n");   // Consume the newline character
    scanf("%[^\n]%*c", ss);

    printf("%c\n", c);
    printf("%s\n", s);
    printf("%s", ss);

    return 0;
}

```

#Description :
this code is used to get char, sentence and group of sentence . program knows when to stop accept input when '\n' is entered.

#Note:
```c
    scanf("%[^\n]%*c", ss);
```
	explain:
		```"%[^\n]``` : This is the format specifier used to read a sequence of characters   until a newline (`'\n'`) character is encountered. The `[^\n]` part specifies a character set that excludes the newline character. In other words, it will read characters until the Enter key is pressed, which signifies the end of the input line. This format specifier is used to capture the entire line of text.
		```%*c```: This part of the format specifier is used to read and discard a single character from the input stream. The asterisk (`*`) before the `%` sign indicates that the character should be read but not stored anywhere.
		
	

```c
void *memset(void *ptr, int value, size_t num);
```

allows you to set a block of memory to a specified value. It is declared in the `string.h` (for C) or `cstring` (for C++) header file. The primary use of `memset` is to initialize memory blocks, often used for arrays, structs, or buffers.
- `ptr`: A pointer to the start of the memory block that you want to fill.
- `value`: The value you want to set each byte of the memory block to. It's an integer value that is converted to an `unsigned char`.
- `num`: The number of bytes you want to fill with the specified value.


```c
getchar();
```
The `getchar` function is a standard C library function used for reading a single character from the standard input stream (usually the keyboard). It is commonly used to read individual characters entered by the user.

-----------
* strstr() ---> to find the first occurrence of a given string in another string?
* if two strings is equal so strcmp() return zero
* strrchr().The library function used to find the last occurrence of a character in a string is

```c

```