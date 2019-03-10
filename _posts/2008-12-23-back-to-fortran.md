---
id: 156
title: やっぱりFortran
date: 2008-12-23T17:54:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/12/23/%e3%82%84%e3%81%a3%e3%81%b1%e3%82%8afortran/'
permalink: /2008/12/23/back-to-fortran/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/12/fortran.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2184170797745082644
categories:
  - コンピュータ
tags:
  - C
  - Fortran
---
<a href="/2008/12/14/him/">HIM</a>に触発されて，C言語を数値計算に使えないかしばらく考えていた．

C言語の文法をおさらい．さまざまな入門書があり，それとは別にポインタの解説が売られている．代入やら繰り返し，変数のような基礎概念を解説しなければならないので，ポインタについては簡単に済ますしかないのかもしれないが，肝心なところをごまかして，2冊目を売ろうというしているのではないかとも思える．プログラミングの基礎は，スクリプト言語でしておくとよいかもしれない．やはり，K&amp;Rの<a href="http://www.amazon.co.jp/gp/product/4320026926?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=4320026926">プログラミング言語C ANSI規格準拠</a>が要領よくまとまっているように思える．Cの基本的な文法自体は難しくなくい．むしろBetter CとされるC++やJavaの方が覚えることが多い．

現在のFortranプログラミングで重要なのは，モジュールと行列．Cはこのあたりが弱い．Cは大域変数の名前空間は基本的にひとつ．ヘッダファイルにマクロ定義をしたり，函数を定義したりして，必要なときにインクルードするというスタイルになる．Fortranだと，useのように陽に指定できる．配列については，多重配列は配列の配列しかないし，添字は0からに限られ，行列式での代入のような便利な機能はない．ポインタとの関係や値渡しの引数には注意が必要．スパコンのコンパイラでは，ポインタは最適化を阻害する要因になりうる．

<a href="http://www.amazon.co.jp/gp/product/4781908683?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=4781908683">UNIXワークステーションによる科学技術計算ハンドブック―基礎篇C言語版</a>のような数値計算の本は，数値計算のアルゴリズムが中心に解説されている．それはそれでよいのだが，よくできているものはライブラリを使うのが普通で，データをいかに処理するかが数値計算の中心．配列のことやモジュール化をどうするか，I/Oについてもっとページを割くべきであるように思う．

Cは簡単な函数を書くにはよさそうだ．Octaveなどで時間がかかる部分を高速化するのに役立つ．グラフィックやシステムの機能を使うプログラムにもよいだろう．しかし，HIMのような大きなものを書くにはCに慣れておかしなことをしないように注意しないといけない．通常は，文法がやさしく，数値計算，データ処理に便利な機能がそろっているFortranを使うのがよいように思う．