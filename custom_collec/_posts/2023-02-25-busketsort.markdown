---
title: Busketsort
type: posts
date: 2023-2-25
categories: [sort]
tags: [sort]
---
{% raw %}

## 思路

使用链表来实现桶内排序  

## *代码如下*

```c++

#include<stdio.h>
#include<stdlib.h>
#include<time.h>

typedef struct _node{
    int num;
    struct _node *next;
}Node;

void swap(int *a,int x,int y){
    int t=a[x];
    a[x]=a[y];
    a[y]=t;
}

void show(int *a,int n){
    int i=0;
    for(;i<n-1;i++)
        printf("%d ",a[i]);
    printf("%d\n",a[i]);
}

void busketsort(int *a,int size,int n){
    Node **busket=(Node**)malloc(sizeof(Node*)*n);
    for(int i=0;i<n;i++){
        busket[i]=(Node*)malloc(sizeof(Node));
        busket[i]->num=0;
        busket[i]->next=NULL;
    }
    
    for(int i=0;i<size;i++){
        Node *node=(Node*)malloc(sizeof(Node));
        node->num=a[i];
        node->next=NULL;
        int f=a[i]/20;
        Node*p=busket[f];
        while(p->next!=NULL&&p->next->num<=node->num){
            p=p->next;
        }
        node->next=p->next;
        p->next=node;
        (busket[f]->num)++;
    }
    Node*s=NULL;
    for(int i=0;i<n;i++){
        s=busket[i]->next;
        for(int j=0;j<busket[i]->num;j++){
            printf("%d ",s->num);
            s=s->next;
        }
        puts("");
    }
    for(int i=0;i<n;i++){
        while((busket[i]->num)--){
            Node*p=busket[i];
            while(p->next!=NULL&&p->next->next!=NULL){
                p=p->next;
            }
            free(p->next);
            p->next=NULL;
        }
        free(busket[i]);
    }
    free(busket);
}

int main(){
    int a[10];
    srand(time(0));
    for(int i=0;i<10;i++)
        a[i]=rand()%100;
    int size=sizeof(a)/sizeof(int);
    show(a,size);
    busketsort(a,size,5);
    return 0;
}
```



{% endraw %}