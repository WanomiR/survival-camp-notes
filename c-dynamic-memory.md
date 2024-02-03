# Dynamic memory allocation
## malloc / calloc
The malloc and calloc functions dynamically request blocks of free memory in a pile.  

Malloc function
```void *malloc(size_t n)```
returns the pointer to n bytes of uninitialized memory, or NULL if the request cannot be satisfied. 

Calloc function ```void *calloc(size_t n, size_t size)``` returns the pointer to an area large enough to store an array of n objects of the specified size, or NULL if the request cannot be satisfied. The allocated memory is set to zeroes by calloc.  

The pointer returned by _malloc_ and _calloc_ will be given with the alignment performed according to the specified object type. However, it can be cast to the appropriate type like in the following code fragment:
```c
int *ip;
ip = (int*) calloc(n, sizeof(int));
```