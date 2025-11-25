# How to run the code
```bash
g++ -o main main.cpp # compile the code
./main # run the code
```

# Pointer
```cpp
int a = 10;
int *p = &a; // p is a pointer to a
cout << *p << endl; // 10
```
The most important and interest thing is it can reach to consecutive memory address.
```cpp
int arr[3] = {1, 2, 3};
int *p = arr;
cout << *p << endl; // 1
cout << *(p+1) << endl; // 2
cout << *(p+2) << endl; // 3
```
Even a slide of array is a pointer.
```cpp
int a[2][4] = {{1,2,3,4}, {5,6,7,8}};
int* b = &a[0][1];
printf("%d\n", b[1]); // 3
```


## Memory Management and Deallocation
5. Memory Management: new and delete

Memory allocated using new needs to be freed using delete to avoid memory leaks.

Release single object:
```cpp
int* s = new int; // allocate memory
*s = 10;          // use memory
delete s;         // free memory
s = nullptr;      // avoid dangling pointer
```
Release array:
```cpp
int* arr = new int[5]; // allocate array memory
// use array
delete[] arr;          // free array memory
arr = nullptr;  
```
