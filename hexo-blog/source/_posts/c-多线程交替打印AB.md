---
title: c++多线程交替打印AB
date: 2022-05-09 15:09:30
tags: [条件变量,多线程]
categories: [c++]
---









-----------------------------

# c++交替打印AB

```c++
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>

using namespace std;

mutex mtx;
condition_variable cond_;
bool flag = true;

void func1(){
    unique_lock<mutex> locker(mtx);
    while(true){
/* 
   调用时, 调用线程会判断条件，如果条件是false，则阻塞并释放锁，如果条件是true，则直接跳过wait执行下面的操作
   如果阻塞，在被其他线程调用notify唤醒后，尝试获取锁，如果获取锁，再判断条件是否满足，如果是true，则继续执行下面的操作，如果是false，则对互斥量解锁，并阻塞该线程
*/
        // 第一次执行由于flag==true不阻塞 
        cond_.wait(locker,[]->bool {return flag;}); // 阻塞时释放锁，执行时获取锁
        flag = false;
        cout<<"AA";
        cond_.notify_one(); // 调用时，线程two被唤醒，但由于线程one还没释放锁，线程two阻塞，等待线程one释放，当线程one再次执行wait,由于flag==flase，所以线程one会被阻塞，同时释放锁，这时线程two获得锁，判断flag==flase，执行下一步，最后又唤醒one，重复如此
    }
}

void func2(){
    unique_lock<mutex> locker(mtx);
    while(true){
        cond_.wait(locker,[]->bool {return !flag;});
        flag = true;
        cout<<"BB";
        cond_.notify_one();
    }    
}

int main(){
    thread one(func1);
    thread two(func2);
    one.join();
    two.join();
    return 0;
}

    
```

