title: InitializaerStruct
date: 2015-12-02 19:27:40
tags:
- C++
description: Struct初始化其实也可以充满艺术
---

<!-- more -->
----
```C++

#include<stdio.h>

typedef struct {
    int z;
} Point;

typedef struct {
    int x;
    int y;
} Point2;

typedef struct {
    Point z;
    Point2 xy;
} Point3;

void printPoint(void* const p,size_t s) {
    int* q = (int*)p;
    size_t n = s / sizeof(int);

    for (size_t i = 0; i < n; i++) {
        printf("%d ", *(q++));
    }
    printf("\n");
}

int main(int argc, char * argv[]) {

    Point p = {1};

    Point2 p1 = { 2, 3};
    Point2 p2 = { .x = 4, .y = 5};

    Point3 p3 = { 6, 7, 8};
    Point3 p4 = { {8}, {6,7}};
    Point3 p5 = { .xy = {6,7} , .z = {8}};
    Point3 p6 = { .xy = {.x=6, .y = 7}, .z = {.z = 8}};
    Point3 p7 = { .xy ={6,7}, .z = {8}};
    Point3 p8 = { xy : {6,7}, z : {8}};

    printPoint(&p, sizeof(Point));

    printPoint(&p1, sizeof(Point2));
    printPoint(&p2, sizeof(Point2));

    printPoint(&p3, sizeof(Point3));
    printPoint(&p4, sizeof(Point3));
    printPoint(&p5, sizeof(Point3));
    printPoint(&p6, sizeof(Point3));
    printPoint(&p7, sizeof(Point3));
    printPoint(&p8, sizeof(Point3));

    return 0;
}
/*
//out put
1 
2 3 
4 5 
6 7 8 
8 6 7 
8 6 7 
8 6 7 
8 6 7 
8 6 7 
Program ended with exit code: 0
*/

```
## 引用
【1】[GNU](https://gcc.gnu.org/onlinedocs/gcc/Designated-Inits.html)