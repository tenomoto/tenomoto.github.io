---
id: 193
title: 数値計算にはFortran
date: 2008-02-05T14:40:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/02/05/%e6%95%b0%e5%80%a4%e8%a8%88%e7%ae%97%e3%81%ab%e3%81%affortran/'
permalink: /2008/02/05/scientic-computing-fortran/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/02/fortran.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1620195453304375327
categories:
  - コンピュータ
tags:
  - Fortran
  - g95
---
半世紀の歴史を持つFortranはCOBOLと並んで, 過去の遺物だと思われている. 大規模な数値計算では, Fortranは現役である. 正確な統計はないが, 地球シミュレータで実行されている大規模な計算のほとんどはFortranで書かれている. Cで書かれているものがいくつかあり, その中には最適化のために一部をFortranで書き直したものがあるそうだ.

パソコンでは, コンパイル不要なスクリプト言語が, さまざまな用途に使われている. パソコンの計算性能が向上し, スクリプト言語でも実用的な計算ができる. しかし, 計算量の大きな問題を解くときは, CやFortranで書いたプログラムの方が圧倒的に速く計算が終了する.

コンパイルは簡単なプログラムならほぼ瞬時に終わるので, プログラムの作成 (修正) と実行のサイクルにおいて, 妨げにはならない. Fortran 77はオブジェクト指向ではないが, サブルーチンは, 十分再利用されてきた. Fortran 90以降はmoduleが導入され, 再利用がしやすくなっている. Fortranは77以前のイメージがつきまとうが, 95, 2003, そして2008と進化を続けている.

スクリプト言語にもさまざまなライブラリへのラッパが提供されていて, 手軽に利用できるようになっているが, CやFortranの資産を利用しているものが多い. それらの資産は, ラッパの作り方の作法を覚えなくても, CやFortranからはそれぞれ直接利用できる. CからFortranのサブルーチンや関数, FortranからCの関数を呼び出すことは, それほど難しくない. CとFortran 77との相互利用の規約はよく知られているし, Fortran 2003ではCとの相互運用性が高められている.

最近ではスクリプト言語での利用も考えて, Cで書かれたライブラリも多い. C99では複素数も使えるようになった. それでは, Cを使うべきだろうか. Cはシステムに近い言語で危険なプログラムが簡単に書ける. また, 配列の機能がFortranに比べて少ない. 基本的な関数を書くにはよいが, 数値計算のプログラムにはFortranが便利である.

JavaはCよりも安全で様々なプラットフォームで動作する. また, 星の数ほどあるフレームワークやライブラリをうまく利用すれば計算結果の可視化ができる. やはりC同様, 配列や入出力がFortranほど手軽に使える形では提供されていないし, 実行速度も劣ることが多い.

Fortran自体には可視化の機能はないが, ライブラリを呼び出すことにより, 簡単な線グラフから3次元グラフィックスまでが可能となる. 大量の数値計算結果を可視化するときには, Fortranの「足腰の強さ」が生きてくる.

数値計算は, 速さが最も重要視されてきたので, ベンダ等が提供する商用コンパイラが主に使われてきた. 近年, gfortranやg95のようなフリーのコンパイラの完成度が高まってきた. フリーのコンパイラは多くのプラットフォームに対応する. コンパイルし直せば同じソースが様々なプラットフォームで利用できる. 同じコンパイラオプションが利用できるのも大きな利点だ.