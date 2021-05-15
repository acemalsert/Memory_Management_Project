# Memory_Management_Project

Design Overview: We used linkedlist as our data structure to point memory adresses. We designed it as a linkedlist that has the attributes size and free_flag and points to the next memory location. We used the help of void pointers a lot since we desired our allocator to be useful with any data type, we also tested our code with several data types. We used the first - fit memory management algorithm in our TEDU_alloc project, since it is the simplest approach and its advantage is to be fast. 

Complete specification: Our allocator first searches a valid place for allocation. In order to allocate place in memory, number of bytes that will be allocated should be smaller than the memory blocks size which we want to allocate and also it shouldn’t be allocated before. If we want a memory location that fits our parameter noOfBytes perfectly, it sets the free_flag to zero and returns the start adress of the block. In case that the block size is bigger than the required memory, we seperate the memory and returns the start adress of that memory block. Here is some description of the functions that we have used: 

void Start(sizeOfRegion): Starts memory with dynamic allocation 

int Mem_Init(int sizeOfRegion) : When we call TEDU_Alloc if the memory isn’t already initialized,it will be called and initialize the memory 

void Seperate(struct mem_block *first_fit_slot,size_t size): To find a free memory block to allocate memory this function uses the "First Fit Algorithm”. Finds a space that has enough memory for our allocation and uses the first one. If we find a memory block for our allocation which fits perfectly, this function is not required. This function will execute only when we have more than required. It takes two arguments respectively; a pointer to mem_block which refers to the mem_block of memory_chunk which has size more than the required size, and required size of the memory_chunk mem_block to be allocated. 

void TEDU_Alloc(size_t noOfBytes): This function allocates the memory according to the number of bytes in the parameter.If memory is not allocated than allocates the memory. We iterate through the allocated blocks and check their size, if the block size is equal to our allocated size and the block is free than we a pointer to that block.If size is smaller than we continue iterating. If size is bigger than we resize that block and return a pointer to that block void Join():This function is for joining the consecutive free blocks. It removes them by removing blocks lying between them.So this function is helpful to minimize wastage of memory. This function is called every time we call the TEDU_Free function. 

int Mem_IsValid(void *ptr): This function checks whether the pointer in the parameter is inside of a memory block.For example if our block is between 1000- 1005 and the pointer is in 1003, than is valid,else, not valid. 

int Mem_GetSize(void * ptr): This function takes a void pointer as parameter. Loops through the list until the end of the list. If Mem_IsValid function returns 1, Mem_GetSize function returns the current size of the current block as bytes, else returns -1. 

int TEDU_GetStats(): This function returns the stats about our memory.How many blocks that we use currently, size of the memory being used and the percentage of the memory that we use compared to the whole memory. 

void TEDU_Free(void * ptr): It takes the void pointer ptr as parameter and frees the memory space pointed to by ptr which must have been returned by a previous call to TEDU_alloc().Otherwise, if free_flag(ptr) has already been called before, undefined behaviour occurs.If ptr is NULL, no operation is performed. 

How our mem.c program runs and functions: We created mem.o object file and libmem.so file as library. In our program we created another c file called mymain.c and imported mem.c file as a library. We made a Makefile in order to run our program. We directly run our mymain.c file which tests the our mem.c file. 

An evaluation of the speed of our program: There are several memory partitioning algorithms available which are used from operating systems to allocate memory. The ones we looked into are First Fit Algorithm, Next Fit Algorithm, Best Fit Algorithm and Quick Fit algorithm.We find out that the fastest one among them is the first-fit algorithm. We wanted our allocator to be as fast as possible. In order to achieve that, we choose the first-fit memory management algorithm in return to wastage of memory. However, we tried to minimize this wastage with some optimization. Our allocator joins consecutive free blocks when we call the TEDU_Free function. So, some of the wasted memory will be regained after we call this function. Known bugs or problems We implemented every function as described and as far as we know, there is no bug or problems in our project.
