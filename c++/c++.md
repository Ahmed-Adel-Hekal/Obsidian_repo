
 ## ranged for : 

``` c++
   int arr [5]= {1,2,3,4,5};
//  Takes more instruction to be excuted good for development
   for(int i: arr){
       std::cout<<i << endl;
    }
// Faster to excute need less instruction check assembly
   for(int i =0 ; i<5 ; i++){
       std::cout<<arr[i] << endl;
    }


```


### Functions

   Function in c++ there is 2 concept 
          1) argument default value                                   2) function overload

when create function prototype you can define default value 
```c++
void fun(int x, int y = 10 ); 

// you cannot do like this

void fun(int x, int y = 10 , int z  );

// if you started to add default value for one of args all next args must have deafault value otherwise it will raise an error

```


2 ) 
 you can define same function with different parameters  type as input this called mangulling 
 each function is defined in assembly as different function and compiler handle which to be called
 ```c++ 
 void sum(int x, int y ); 
 void sum(int x, float y);

// note that return type must be the same

```

----
## Refrence :
Not like pointer it is just another name for same thing.

```c++
int x = 10 ;
int &y = x ; // reference
int * ptr  = &x ; // pointer to x variable
```

if you didnot give it value it will cause compiler error 

---
## auto 
unlike c auto is way to create var without explicit define it is type. 
```c++ 
auto x = 10 ; 
// no need to define type of x
```


---
## const 
in c *const* is external linkage means that you can define it in file and give it value in other file and link this 2 files together 
in c++ if you have cost value you have to give it value other wise it will cause error 
```c++ 
const in ll ; 
// this will cause error 
const int ll =0 ; 
// it will work with no errors
```

in c you cannot have case in switch must be const expression not const var in c++ it is allowed to have case with const var

```c++
const int x = 0 
int var =  0 ; 
switch(var){
case x :
std::cout << "const case" << std::endl ;  
}
```

you can use const expression in array 
```c++ 
const_num = 2 
int arr[const_num] = {1,2};
// this will not case any error
```

you  cannot use pointer to const it will case error you will need to cast it. 
```c++ 
const int x = 1 ; 
int *ptr = &x ; 
// this will case error 
```

---
## struct 

```c++ 


struct test {
	int y = 10 ;
	void fun3(){
	std::cout << "world " << std::endl ; 
	}
	
};

struct data :test {
	int x = 3 ;
	void fun(){
	std::cout << "hello " << std::endl ;
	std::cout << y << std::endl ; 
	}
	
};

main(){

	data d ;
d.fun();
d.fun3();
}


```



-----
## Enum 

```c++

enum data{
sucess,
fail
};

int main(){

data d ; 
std::cout << d<< endl ; 

// convertion from int to enum is forbidden and cause error 
// data d = 2 ; 
// this will cause error 
// otherwise it will work  except class enum 
// int x = fail ; 
// Diffrent enum with same value 

// 
}
```