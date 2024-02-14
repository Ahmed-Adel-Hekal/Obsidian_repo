```c
// stringizing operator
# define print(x) (printf("%s",#x))

int main(){
print(hello);
}
```

```c
# define multi(a,b) a*b
int main(){
printf("%d", multi(1+2,2+3));
}
```
```c 
# define printcv()  printf("Ahmed Adel");\
					printf("Age : 30");\
					printf("Graduated S");

int main(){
	int x = 1 ;
	if(x ==1)printcv();
	else printf("Error");
}
```