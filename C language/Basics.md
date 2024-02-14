

- C is week programming language as we can perform type conversion 
- Register keyword work with only basic data types , local variables & fun ction argument.
- **C Keywords**
*Const* : when init can not be modified 
*extern*: Extend visability of variable to be used between files in c
```c
///////////////////// File A   ////////////////////
int x ; 

/////////////////////   File B ////////////////////
extern int x ; // is ok 
extern int x = 5 ; // this will cause linking error you provide 2 initializer of x   
```
*static*: Extend variable life time 
*global*: var can be declared again when first declaration doesn't initialize the var 
```c
////////// this will be ok 
int x ; 
int x = 5 ; 
int main (){
printf("%d", x); 
}

///////// this will cause error

int main (){
int x ; 
int x =5 ; 
printf("%d", x); 
}
```


---------------------
```c
	char a = 0xfb ;
	unsigned char b = 0xfb ;
	if (a==b)
	printf("equal");
	else
	printf("not equal");

/// output not equal 
```
------
***Scanf_Tricks***
```c
/* A simple scanset example */
#include <stdio.h>
 
int main(void)
{
    char str[128];
 // will accept capital letter if name start with small letter it will have random value
 // it will take capital and if there small letter it will stop taking arg
    printf("Enter a string: ");
    scanf("%[A-Z]s", str);
 
    printf("You entered: %s\n", str);
	

// it will scan all letter untill reach o 
// input :.mohamed
// output :. m  
 
    printf("Enter a string: ");
    scanf("%[^o]s", str);
 
    printf("You entered: %s\n", str);
	
	// will take all input untill you hit enter
	printf("Enter a string with spaces: ");
    scanf("%[^\n]s", str);
 
    printf("You entered: %s\n", str);
 
 
    return 0;
}
```

-----
***Printf_tricks***
```c
int main()
{
	printf("%c",6["Ahmed ADel"]);
	printf("%c","Ahmed ADel"[6]);

}
//// output is AA
```

----------
***Basic_Tricks***
```c
int main()
{
	int a = 7/22*(3.14+2)*3/5 ;
	printf("%d",a);
}
///////////////////////
int main()
{
	int a = 4+2%-8 ;
	printf("%d",a);
}
/////////////////////////
int main()
{
	unsigned int x = -1 ;
	int y = ~0 ;
	if(x==y)
		printf("same");
	else
		printf("not same");
}
/////////////////////////
int main()
{
	int i=5, j=10, k=15;
	printf("%d", sizeof(k/=i+j));
	printf("%d",k);
}
////////////////////////////
int main()
{
	int a =10 , b =20, c=30;
	if(c>b>a)
		printf("True");
	else
		printf("False");
}
///////////////////////////////////
int main()
{
	int a,b,c;
	 a=b=c= 10;
	if (a==b==c)
		printf("True");
	else
		printf("False");

}
/////////////////////////////////////
// Remeber logical operation evaluated left to right ////
int main()
{
	int i=1;
	if (i++&&(i==1))

		printf("True");
	else
		printf("False");

}
///////////////////////////////////////
/// compiler dependent 

int main()
{
	int a =1 ;
	int b = 0 ;
	b  = a++ + a++ ;
	printf("%d  %d",a,b);

}
////////////////////////////////////////////
// cause error as modulos is allowed for int only
// use fmod()
int main(){  
float num1=2.5,num2=1.5;  
float num3=num1%num2;  
printf("num3=%d",num3);  
return 0 } 
////////////////////////////////////////////

```


***Types of Sections in C***

- Allocatable : (Only found in Flash)           * Loadable: (Copy taken from flash to Ram)

.data  ---> loadable                        .bss ---> loadable
.Text ---> depends on compiler but most is allocatable 
.rodata ---> it depends 

.Bss ---> will nor reserve any memory in ram but it will replace variable with Push instruction 


***Startup code***

1- Load (.data) variable from flash to Ram.
2- Allocate (.bss) in Ram & initialize them ot zero 
3 call main or what ever function to start 