
* Three ways to use #pragma
```c 
// first 
typedef struct{
	int x ; 
} test __attribute_((packed)); 
// second 
#pragma pack(1) 
typedef struct{
	int x ; 
} test;
// third 
#pragma pack(push,1) 
typedef struct{
	int x ; 
} test;
#pragma pack(pop)

```