---
id: 187
title: 最初のプログラム
date: 2008-02-14T16:35:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/02/14/%e6%9c%80%e5%88%9d%e3%81%ae%e3%83%97%e3%83%ad%e3%82%b0%e3%83%a9%e3%83%a0/'
permalink: /2008/02/14/circle-area/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/02/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8082598230801804983
categories:
  - コンピュータ
tags:
  - Fortran
  - g95
---
半径を入力して円の面積を求めるプログラムは次の通り.

```fortran
program area
 implicit none

 real, parameter :: pi = 3.14159
 real :: r

 print *, "Enter radius"
 read *, r
 print *, "radius=", r, "area=", pi*r**2
end program area
```

プログラムは`program`で始まり, `end program`で終わる. プログラム名をここでは`area`とした. `implicit none`は全ての変数を陽に宣言することを示している. Fortranでは, 宣言なしに変数を使うこともできるが, バグを防止するため, `implicit none`は必ずつけるようにする.

`real`は実数の宣言. `parameter`は定数であるという属性. 変数rにキーボードから値を入力してもらい結果を表示する.

入力を促すprint文だけでなく, 確認のため入力された値を表示すると間違えが少なくなる.

大規模なプログラムであれば, namelist入出力を利用したり, コマンドラインツールを作るときは, コマンドライン引数を利用することがよい. 簡単なプログラムでは, print, read, printの組み合わせで対話的なプログラムを作る方が状態がひとつひとつ確認できるので便利である.