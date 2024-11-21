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


## 内存管理和释放
5. 内存管理：new 与 delete

使用 new 分配的内存需要使用 delete 释放，以避免内存泄漏。

释放单个对象：
```cpp
int* s = new int; // 分配内存
*s = 10;          // 使用内存
delete s;         // 释放内存
s = nullptr;      // 避免悬挂指针
```
释放数组：
```cpp
int* arr = new int[5]; // 分配数组内存
// 使用数组
delete[] arr;          // 释放数组内存
arr = nullptr;  
```
