* pointer size is equal to size of memory locations (address bus)

char *ptr = 0x50 ; ----> is number 
char *ptr = (char *)0x50 --> is address

------------------------------------------
	Difference of two same type of pointer is always one.
 
	 *++ptr ----> increment pointer then derefrence
	*ptr++ ---> first derefrence then increment pointer 
	++*ptr ---> increment value at current position then derefrence
	(*ptr)++ --> derefrence then increment value

---
```c
    int arr [3][4]= {1,11,3,4,5,6,7,8,9,10,11,12};\

    printf("%u    %u    %u ",arr[0]+1,*(arr[0]+1) ,*(*(arr+0)+1));
/// address  11    11
```

```c
    int arr [2][3]= {5,10,15,20,25,30};
    int (*ptr)[2][3] = &arr ;

    printf("%d    %d    %d ",***ptr,***(ptr+1) ,*(*(*ptr+1)+2));
    ///  5  address 30
```

```c
str[7], 7[str] is equal to 
*s = str ; 
*(s+7) is equal *(7+s)
```

```c
str[]="peace"; char *s = str; //s+3 --> ce  // s+++3---> ce // ++s+3 -->e 
```

```c
i>45 ? return x : return y ; 
// this will be compiler error as ternary operation cannot be used with return 
```

```c
char *ptr = "geeks"; printf("%c",*&*&*ptr);
// g
```

```c
void fun(int arr[]){
int i ; 
int size = sizeof(arr)/sizeof(arr[0]);
for(int i = 0; i< size ; i++)
printf("%d",arr[i]);
}
// this will not cal arr size as array is passed as pointer so 
sizeof(arr)--> sizeof pointer not array 
sizeof(arr[0])--> size of first element in array 
so output depend on platform 
```

```c
void swap(char **x,char** y ){

    char *t = *x;
    *x = *y;
    *y = t;
}

int main()
{
	char *s = "Ahemd";
	char *z = "Hekal";
	swap(&s,&z);
	printf("%s",s);
    return 0;
}

```

---
```c
char *str = "yassin";
str = "mohamed";   str[0]='x' ; 
// we can change what pointer points to 
// but we can't change it is content
///////////////////////////////////////////
char str[] = "yassin";
str = "mohamed";   str[0]='x' ; 
// str is const pointer so it cannot be changed
// but can be modified 
```
---
```c
int (*ptr)[2][3] -- > pointer points to all array so ptr ++ will be out of array range 
-------------------------------------------
int (*arr)[2]  --> this will points to each ro so arr++ will increment by row
so (*arr)[i] to print element by element 
-------------------------------------------
*(arr+1)[1] == *(arr+2)
```
---
```c
int sum(static int x) ---> will cause error as func arg cannot used with storage specifier except register  
```
---
`* cannot perform arthmitics operation on void pointer as we donot know how to derefrence

----
```c
char g[] = "geeksforgeeks";
printf("%s", g+g[6]-g[8]); // equals to g[8] as ascii of O = ascii of g 
// will be 8
```