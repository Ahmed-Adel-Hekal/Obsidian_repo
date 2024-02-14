
```c 
int main(){
	if (sizeof(int)>-1){
	printf("True");
	}
	else{
	printf("False");
	}

}
```

code output is `Flase` please refer to the 2's coplement presentation for -1

-----
```c
int main(){

	flaot f = .1;
	if (f == .1){
	printf("True");
	}
	else{
	printf("False")
	}
}
```

output is `False` .1 is presented as double and f is `float`

-----
```c
int main()
{
	int a,b=1, c=1 ; 
	a = sizeof(c=++b +a);
	printf("%d  %d  %d", a,b,c);
}
```

code Output is `4   1   1 `  as `sizeof()` is operator c will not be assigned


----
```c
int main(){

	char *p = 0 ;
	*p = 'AA';
	printf("Value at p = %c", *p); 
}
```

code Output is `Segmentation error(core dump)` as you try to assign value to pointer that has  address of 0 which is illegal memory to write to.
core dump happens when ever you have illegal access. 

----
```c
int main (){
	 int a = 1 , b =3 , c = 2 ;
	 if (a>b)
		 if(b>c)
			 printf("a > b and b > c");
	else 
	printf("Something is wrong");
}
```

code Output is ` ` simply nothing as else belongs to second if .

-------------
```c
int main() {

	long double a ;
	signed char b ;
	int arr [sizeof(!b+a)];
	printf("%d",sizeof(arr));

}
//!b will be promoted to be int then int + long double which equals to 
// long double which equals 12 
//output will be 12 * 4 = 48

int main() {

	long double a ;
	signed char b ;
	int arr [sizeof(!a+b)];
	printf("%d",sizeof(arr));

}
//!b will be depromoted to be int which equals to 4 
//output will be 4 * 4 = 16

```



