---
emoji: ๐ช
title: (์๊ณ ๋ฆฌ์ฆ) Double Linked List C++ ๊ตฌํ ์๊ณ ๋ฆฌ์ฆ
date: '2019-06-29 04:00:00'
author: ์ค์ฝ๋ฉ
tags: algorithm
categories: ์๊ณ ๋ฆฌ์ฆ
---

## ๋งํฌ๋ ๋ฆฌ์คํธ

๋งํฌ๋ ๋ฆฌ์คํธ๋ ๋์ ์ค๋ ์์ ์ด๋ค. ํญ์ ์ตํ์ ๋ฐฉ๋ฒ์ผ๋ก ๋ฏธ๋ค๋๋ ๋ฐฉ๋ฒ์ธ๋ฐ ์๊ณ ๋ฆฌ์ฆ์ ํ๋ฉด์ ๋งํฌ๋ ๋ฆฌ์คํธ๋ฅผ ์ฌ์ฉํ์ง ์๊ณ ๋ ํ๊ธฐ ์ด๋ ค์ด ๋ฌธ์ ๊ฐ ๋์์ ํ๋ ์ ์์ด ์ ๋ฆฌ๋ฅผ ํด๋ณธ๋คใใ

## ๋๋ธ ๋งํฌ๋ ๋ฆฌ์คํธ๋?

๋ณดํต ๋งํฌ๋ ๋ฆฌ์คํธ๋ผ๊ณ  ํ๋ฉด ๋ค์ ์์๊ฐ ๋ฌด์์ธ์ง(next)๋ฅผ ํฌ์ธํฐ๋ก ์ฐ๊ฒฐํด๋๊ฒ ๋๋ค. ํ์ง๋ง ๋๋ธ ๋งํฌ๋ ๋ฆฌ์คํธ๋ ์ด์  ์์์ ๊ฐ๋ ์๋ ค์ฃผ๋(prev) ํฌ์ธํฐ๊ฐ ์กด์ฌํ๋ค.

๋๋ธ ๋งํฌ๋ ๋ฆฌ์คํธ๋ ์ง๊ธ element ์ดํ์ ์ด์ ์ ์์ ์ ๋ณด๊ฐ ๋ชจ๋ ํ์ํ  ๋ ์ฌ์ฉํ๋ค.

ex) **์์ ์ ๋ฐฉํฅ, ์ญ๋ฐฉํฅ์ผ๋ก ์ถ๋ ฅํ๊ธฐ**

## ์ฐธ๊ณ 

[๋๋ธ ๋งํฌ๋ ๋ฆฌ์คํธ ์ฐธ๊ณ  ์ฌ์ดํธ](https://hijuworld.tistory.com/55)

**์ฌ๊ธฐ์ tail์ด ์์ง์ผ ์ ์๊ฒ ์ฝ๋๋ฅผ ์์ ํ๋ค.**

## Node ๊ตฌ์กฐ์ฒด

Node๋ฅผ ์ถ๊ฐํ  ๋๋ ptr ์ ๋ณด๋ฅผ ๊ฐ์ด ๋ฐ์์์ ptr ๋ฐ๋ก ๋ค์๋ค๊ฐ ์๋ก ์์ฑ๋ ๋ธ๋๋ฅผ ์ฐ๊ฒฐ์์ผ์ค๋ค.

```cpp
struct Node {
    char data = ' ';
    Node* next, * prev;
    Node() {
        next = prev = NULL;
        data = ' ';
    }
    Node(char c, Node* ptr)//ptr ๋ค์ ์ถ๊ฐ
    {
        data = c;
        prev = ptr;
        next = ptr->next;
        next->prev = prev->next = this;
    }
    void selvDelete() {
        prev->next = next;
        next->prev = prev;
        delete this;
    }
};
```

## Double Linked List ๊ตฌ์กฐ์ฒด

๋๋ธ ๋งํฌ๋ ๋ฆฌ์คํธ์์ ๋๋ฏธ๋ฅผ head์ tail์ ๋๋ฌ์ ๋งํฌ๋ ๋ฆฌ์คํธ๊ฐ ๋ฒ์๋ฅผ ์ด๊ณผํ์ง ์์ ์ ์๊ฒ ๋์์ค๋ค.

- ์๋ก์ด ์์๊ฐ ์ถ๊ฐ๋  ๋๋ tail ์์ ์ถ๊ฐ ํด์ฃผ๊ณ (์ถ๊ฐ ํ์๋ tail ๋ค์ ์๋ ์์๋ ๋์ผํ๋ค)
- tail์ ์์ง์ผ ์ ์๊ฒ ํด์ ์ค๊ฐ์ ์์๋ฅผ ์ถ๊ฐํ๊ฑฐ๋ ์ญ์ ํ  ์ ์๊ฒ ํด์ฃผ์๋ค.
- ์ถ๋ ฅ์ head๊ฐ ๋๋ฏธ์ด๊ธฐ ๋๋ฌธ์ head ๋ค์ ์์๋ถํฐ ๋ ์์๊น์ง

```cpp
struct DLinkedList {
    Node *head;
    Node *tail;
    int count;
    DLinkedList() { //์์ฑ์
        count = 0;
        head = new Node(); //๋๋ฏธ๋ฅผ ์ ์ธํด์ ๊ฐ์ง๊ณ  ์๊ฒํ๋ค.
        tail = new Node(); //๋๋ฏธ๋ฅผ ์ ์ธํด์ ๊ฐ์ง๊ณ  ์๊ฒํ๋ค.
        head->next = tail; //์๋ก์ฐ๊ฒฐํ๋ค.
        tail->prev = head;
    }
    void endInsert(char c) { //tail ์์ ์ถ๊ฐํ๋ค.
    new Node(c, tail->prev);
    }
    void moveRight(){
    if (tail -> data == ' ') return;
    tail = tail -> next;
    }
    void moveLeft(){
    if (tail->prev == head) return;
    tail = tail -> prev;
    }
    void endDelete() { //tail ์์ ์ ๊ฑฐํ๋ค.
    if (tail->prev == head) return;
    tail->prev->selvDelete();
    }
    void printAll() {
        Node* tmp = head;
        while (tmp->next != NULL) {
            cout<< tmp->next->data;
            tmp = tmp->next;
        }
    }
};
```

## ์ต์ข ์์  ์ฝ๋(๋ฐฑ์ค 1406๋ฒ)

```cpp
#include <string>
#include <iostream>
#include <vector>
#include <cstdlib>

using namespace std;

struct Node {
    char data = ' ';
    Node* next, * prev;
    Node() {
        next = prev = NULL;
        data = ' ';
    }
    Node(char c, Node* ptr)//ptr ๋ค์ ์ถ๊ฐ
    {
        data = c;
        prev = ptr;
        next = ptr->next;
        next->prev = prev->next = this;
    }
    void selvDelete() {
        prev->next = next;
        next->prev = prev;
        delete this;
    }
};

struct DLinkedList {
    Node *head;
    Node *tail;
    int count;
    DLinkedList() { //์์ฑ์
        count = 0;
        head = new Node(); //๋๋ฏธ๋ฅผ ์ ์ธํด์ ๊ฐ์ง๊ณ  ์๊ฒํ๋ค.
        tail = new Node(); //๋๋ฏธ๋ฅผ ์ ์ธํด์ ๊ฐ์ง๊ณ  ์๊ฒํ๋ค.
        head->next = tail; //์๋ก์ฐ๊ฒฐํ๋ค.
        tail->prev = head;
    }
    void endInsert(char c) { //tail ์์ ์ถ๊ฐํ๋ค.
        new Node(c, tail->prev);
    }
    void moveRight(){
        if (tail -> data == ' ') return;
        tail = tail -> next;
    }
    void moveLeft(){
        if (tail->prev == head) return;
        tail = tail -> prev;
    }
    void endDelete() { //tail ์์ ์ ๊ฑฐํ๋ค.
        if (tail->prev == head) return;
        tail->prev->selvDelete();
    }
    void printAll() {
        Node* tmp = head;
        while (tmp->next != NULL) {
            cout<< tmp->next->data;
            tmp = tmp->next;
        }
    }
};

int main(){
    DLinkedList *list = new DLinkedList();
    int n;
    char cmd, input;
    cin >> n;

    for(int i = 0; i < n; i++){
        cin >> cmd;
        if(cmd == 'P'){
            cin >> input;
            list->endInsert(input);
        }
        else if(cmd == 'D'){
            list->moveRight();
        }
        else if(cmd == 'B'){
            list->endDelete();
        }
        else if(cmd == 'L'){
            list->moveLeft();
        }
    }
    list->printAll();
}
```

## ์ฃผ์ํ ์ 

- ๋งํฌ๋ ๋ฆฌ์คํธ ๋ฌธ์ ๋ ์๋ฌด๋ฆฌ ๊ฐ๋จํ ๋ฌธ์ ๋ผ๋ ๊ทธ๋ฆฌ์ ์ ๋ฐ...
- ์ ๋ฐ ์ฝ๋ค๊ณ  ๋ง ์ง์ง ๋ง์์ใ ใ ใ 
