---
id: 60
title: TeXのソースを分割してTeXShopでタイプセット
date: 2012-04-03T09:30:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/04/03/tex%e3%81%ae%e3%82%bd%e3%83%bc%e3%82%b9%e3%82%92%e5%88%86%e5%89%b2%e3%81%97%e3%81%a6texshop%e3%81%a7%e3%82%bf%e3%82%a4%e3%83%97%e3%82%bb%e3%83%83%e3%83%88/'
permalink: /2012/04/03/tex-source-division-texshop-typeset/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/04/textexshop.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6175617456803528037
categories:
  - コンピュータ
tags:
  - Mac
  - TeX
  - TeXShop
---
長い書き物をするとき、TeXのソースはいくつかのファイルに分割することが多い。
<!--more-->

ルートファイルroot.texにinput{foo}を使って、foo.texの中身を取り込む。
コマンドラインだとMakefileに依存関係を書いておくと楽。でも、ちょっと面倒。<a href="http://d.hatena.ne.jp/hayamiz/20081208/1228727272">omake</a>で更新のたびに自動的にタイプセットすることもできる。
<a href="http://pages.uoregon.edu/koch/texshop/">TeXShop</a>では、foo.texを編集しているときにタイプセットをクリック、またはCommand+Tしてfoo.tex自体をコンパイルしてしまうことがある。
foo.texの冒頭に
<pre>%!TEX root = root.tex</pre>
と書いておくと、foo.texの代わりにroot.texをコンパイルする。
root.texには
<pre>%!TEX TS-program = pdflatex</pre>
のようにどのコマンドでタイプセットするか書いておくとよい。
どちらもTeXShopのヘルプに書いてある。