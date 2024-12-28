实验七 指针 
一、实验目的 
1、熟练掌握指针、地址、指针类型、void指针、空指针等概念。 
2、熟练掌握指针变量的定义和初始化、指针的间接访问、指针的加减运算和指针表达式。 
3、会使用数组的指针和指向数组的指针变量。 
4、会使用字符串的指针和指向字符串的指针变量。 
二、实验准备 
1、复习变量、变量的地址、指针变量的概念并明确区分这三个不同的概念。 
2、复习指针和数组的结合应用。 
3、复习指针的其他理论知识。 
三、实验内容 
1、阅读程序，分析可能产生的结果，并在机器上运行。 
#include <stdio.h> 
void main() 
{ 
int i,*p; 
p=&i; 
*p=5; 
printf("%d\n",i); 
printf("%d\n",*p); 
printf("%d\n",p); 
printf("%d\n",&i); 
} 
回答;可能会出现返回类型不匹配,格式说明符不匹配,指针解引用混淆,变量与地址混淆等问
题 
![image](https://github.com/user-attachments/assets/975a5e2b-4696-4bc7-bb61-dbc9506caa9d)

2、用指针对n个整数进行排序，并将结果顺序输出。要求排序用一个函数实现，主函数只
输入n个整数和输出已排序的n个整数。 
#include <stdio.h>
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
void bubbleSort(int *arr, int n) {
    int i, j;
    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j]>arr[j + 1]) {
                swap(&arr[j], &arr[j + 1]);
            }
        }
    }
}
int main() {
    int n, i;
    printf("请输入整数的个数n: ");
    scanf("%d", &n);
    int arr[n];
    printf("请输入%d个整数:\n", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    bubbleSort(arr, n);
    printf("排序后的结果为:\n");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    return 0;
}
![image](https://github.com/user-attachments/assets/ccef124d-5a3c-4662-ac89-895fed78edf9)

3、编写一个函数alloc(n)，用来在内存新开辟一个连续的空间（n个字节）。再写一个函数
free(p)，将以地址p开始的各单元释放。主程序输入10个不等长的大写字符串，每输入一
个字符串，应放在新申请的一片连续的空间。该字符串反序输出后，释放它所占用的空间。
#include <stdio.h>
#define ALLOCSIZE 1000
char allocbuf[ALLOCSIZE];
char *palloc = allocbuf;
char *alloc(int n) {
    if (palloc + n <= allocbuf+ALLOCSIZE) {
        char *result = palloc;
        palloc += n;
        return result;
    } else {
        return NULL;
    }
}
void free(char *p) {
    if (p >= allocbuf && p < allocbuf + ALLOCSIZE) {
        palloc = p;
    }
}
#include <stdio.h>
#include <string.h>

int main() {
    int i;
    for (i = 0; i < 10; i++) {
        char str[100];
        scanf("%s", str);
        int len = strlen(str);
        char *space = alloc(len + 1);
        if (space!= NULL) {
            int j;
            for (j = 0; j < len; j++) {
                space[j]=str[len - 1 - j];
            }
            space[len]='\0';
            printf("%s\n", space);
            free(space);
        } else {
            printf("内存不足，无法分配空间\n");
        }
    }
    return 0;
}
![image](https://github.com/user-attachments/assets/c70e770a-0c94-4f94-a17f-4aace3822769)
