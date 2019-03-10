---
id: 220
title: 今更Make本
date: 2007-03-07T22:35:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2007/03/07/%e4%bb%8a%e6%9b%b4make%e6%9c%ac/'
permalink: /2007/03/07/oreilly-make/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/03/make.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8349830521100214423
categories:
  - コンピュータ
  - 書評
tags:
  - Make
---
オライリーの<a href="http://www.amazon.co.jp/gp/product/4873112699?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=1211&amp;creativeASIN=4873112699">GNU Make</a>を買った．

8年ほど前にManaging projects with Makeを買ったが，GNU Makeでないとコンパイルできないものがあるという程度の認識だった．依存関係の順序が逆転する（.f.oなど）サフィックス・ルールは古くて，より自 然なパターン・ルール（%.o : %.f）を使うことはもちろん，実は.PhonyターゲットやVPATHもよく分かっていなかった．便利かもしれないけどいつも使えるとは限らない拡張機 能を多用しているという先入観があったが，GNU Makeはもはやスタンタードなので，これを機会に勉強してみよう．