---
id: 138
title: C++でHello, World!
date: 2009-03-09T19:51:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/09/c%e3%81%a7hello-world/'
permalink: /2009/03/09/cxx-hello-world/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/ck.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/9207236344674911128
categories:
  - コンピュータ
tags:
  - C
---
<!--more-->

```c++
#include <iostream>
using namespace std;

int main()
{
    std::cout << "Hello, World!" << std::endl;
}
```

名前空間std::が必要な今日この頃．