---
layout: post
title:  "shared_ptr智能指针"
date:   2015-11-19
categories: C++
---

# shared_ptr智能指针说明

shared_ptr是最像指针的智能指针，是boost.smart_ptr库中最重要的部分。shared_ptr与scoped_ptr一样，包装了new操作符在堆上分配的动态对象，但其实现的是引用计数型的智能指针，可以被自由地拷贝和赋值，在任意的地方共享它。当没有代码使用（即引用计数为0）时，删除被包装的动态分配的对象。shared_ptr可放到标准容器中，并弥补了auto_ptr因为转移语义而不能把指针作为STL容器元素的缺陷。

## shared_ptr线程安全性

- 一个shared_ptr实体可被多个线程同时读取
- 两个的shared_ptr实体，可被两个线程同时写入，析构为写操作
- 如果要从多个线程读写同一个shared_prt对象，则需要枷锁

## shared_ptr用法

    shared_ptr<int> sp(new int(10));        // 指向整数的shared_ptr
    assert(sp.unique());                             // shared_ptr是指针的唯一持有者
    shared_prt<int> sp2 = sp;                   // 第二个shared_ptr，拷贝构造函数
    assert( sp == sp2 && sp.use_count() == 2);      //两个shared_ptr相等，指向同一个对象，引用计数为2
    *sp2 = 100;                                         // 修改被指对象
    assert( *sp == 100)                             // 另一个shared_ptr也同时被修改
    sp.reset();                                           // 停止shared_ptr的使用
    
## shared_ptr应用于标准容器

有两种方式将shared_ptr应用与标准容器

1. 将容器作为shared_ptr管理的对象，如`shared_ptr< list<T> >`，使容器可以被安全地共享，用法与普通shared_ptr没有区别

2. 另一种用法是将shared_ptr作为容器元素，如`vector< shared_ptr<T> >`，因为shared_ptr支持拷贝语义与比较操作，符合标准容器对元素的要求yi 可实现在容器中安全地容纳元素的指针而不是拷贝

标准容器不能容纳auto_ptr，这个为C++标准特别规定的。同样，标准容器也不能容纳scoped_ptr

存储shared_ptr的容器与存储原始指针的容器功能几乎一样，单shared_ptr为程序员做了指针的管理工作，可以任意使用shared_ptr，而不用担心资源泄露

    vector< shared_ptr<int> > v(10);
    
## shared_ptr特点

scoped_ptr虽然简单医用，但是其不能共享所有权的特性却大大限制了其使用范围，而shared_ptr则为可以共享所有权的智能指针。

shared_ptr指针如果有两个指针，则同时拥有了某对象的访问权限，当两个指针都释放对该对象的所有权时，其所管理的对象的内存才被自动释放。在共享对象的访问权限时，也实现了其内存的自动管理。

shared_ptr的管理机制为，对所管理的对象进行引用计数，当新增一个shared_ptr对该对象进行管理时，就将该对象的引用计数加一；当该对象的引用计数为0时，说明没有任何指针对其管理，才调用delete释放其所占的内存

避免对shared_ptr所管理的对象的直接内存管理操作，以免造成该对象的重释放；shared_ptr不能对循环引用的对象内存自动管理

另外，不要构造一个临时的shared_ptr作为函数的参数。以下用法可能导致内存泄露

    void test()
    {   foo( boost::shared_ptr<class>( new class() ), g() );}      