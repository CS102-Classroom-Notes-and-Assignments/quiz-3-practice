# quiz-3-practice

Review of pointers and arrays: https://www.youtube.com/watch?v=ASVB8KAFypk

### General Questions
1. What is a pointer?
2. Why should we use pointers?
3. How are pointers and arrays related?
4. What data type should a pointer be?

### Pointer Code Questions
- Draw out the diagrams explaining the pointers below (feel free to use dummy address values). What does the code print out at each step?
```c
#include <stdio.h>

int main()
{
    int x=1, y=2, z[10];
    int *ip;            // ip is a pointer to an int

    ip = &x;            // ip now points to x
    printf("ip=%x\n", ip);   // prints address of x

    y = *ip;            // y is now 1
    printf("y=%d\n", y);

    *ip = 0;            // x is now 0
    printf("x=%d\n", x);

    ip = &z[0];         // ip now points to z[0]
    printf("ip=%x\n", ip);

    return 0;
}
```
##### Answer:
<img src="pointers_1.png" width="400">

https://www.dropbox.com/s/vl5ppwjrwrt2uhl/pointer_example_1.mp4?dl=0


#### Pointer Unary Operators * and & with arithmetic operators
- What does the following code print out?
```c
#include <stdio.h>

void printArray(int arr[])
{
    for (int i=0; i<10; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

void printArrayAddress(int arr[])
{
    for (int i=0; i<10; i++)
        printf("%x ", &arr[i]);
    printf("\n");
}

int main()
{
    int intArr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    printArray(intArr);
    printArrayAddress(intArr);

    int *intPtr = intArr;           // defaults to &intArr[0]
    printf("intPtr=%x\n", intPtr);
    printf("*intPtr=%d\n", *intPtr);

    int *intPtr2 = &intArr[2];      // address of intArr[2]
    printf("intPtr2=%x\n", intPtr2);
    printf("*intPtr2=%d\n", *intPtr2);

    printf("\n");

    *intPtr2 = *intPtr2 + 10;       // adds 10 to arr[2]
    printf("intPtr2=%x\n", intPtr2);
    printf("*intPtr=%d\n", *intPtr2);

    int y;
    y = *intPtr2 + 1;               // gets arr[2] and adds 1
    printf("y=%d\n", y);

    *intPtr2 += 10;                 // adds 10 to arr[2]
    y = *intPtr2;
    printf("y=%d\n", y);

    ++*intPtr2;                     // adds 1 to arr[2]
    y = *intPtr2;
    printf("y=%d\n", y);

    (*intPtr2)++;                   // adds 1 to arr[2]
    y = *intPtr2;
    printf("y=%d\n", y);

    *intPtr2++;                     // increments pointer to arr[3]! That's it!
    y = *intPtr2;
    printf("y=%d\n", y);
    return 0;
}
```
##### Answer:
<img src="pointers_2.png" width="400">

https://www.dropbox.com/s/uz2nz19gbqby2ol/pointer_example2.mp4?dl=0

## Pointers and Function Arguments
Review of Swap: https://www.youtube.com/watch?v=qz_iz_PLorc

C passes arguments to functions by value, so there is no direct way for the function to alter a variable in the calling function. 

#### Wrong Swap
```c
#include <stdio.h>

// K&R Pg. 95
void swap(int x, int y)
{
    int temp;

    temp = x;
    x = y;
    y = temp;
}

int main()
{
    int x = 1;
    int y = 2;
    printf("before: x=%d, y=%d\n", x, y);

    swap(x, y);
    printf("after:  x=%d, y=%d\n", x, y);
}
```
#### Correct Swap
```c
#include <stdio.h>

// K&R Pg. 96
void swap(int *px, int *py)
{
    int temp;

    temp = *px;
    *px = *py;
    *py = temp;
}

int main()
{
    int x = 1;
    int y = 2;
    printf("before: x=%d, y=%d\n", x, y);

    swap(&x, &y);
    printf("after:  x=%d, y=%d\n", x, y);
}
```


## Pointers and Arrays
Any operation that can be achieved by array subscripting can also be done with pointers. 
```c
int a[10];
int *pa;
pa = &a[0]; 	// pa contains the address of a[0]
x = *pa;	// copy the contents of a[0] into x
```

If pa points to a particular element of an array, then by definition pa+1 points to the next element, pa+i points i elements after pa, and pa-i points i elements before. Thus, if pa points to a[0], *(pa+1) refers to the contents of a[1], pa+i is the address of a[i], and *(pa+i) is the contents of a[i].
These remarks are true regardless of the type or size of the variables in the array a.

Thus after the assignment 
```pa =&a[0];```
pa and a have identical values. Since the **name of an array is a synonym for the location of the initial element**, the assignment ```pa=&a[0]``` can also be written as 
```pa=a;```

Similarly ```a[i]``` is the same as ```*(a+i)```. The two forms are equivalent in C. 

Practice using ```a[i]``` and ```*(a+i)``` in code.
