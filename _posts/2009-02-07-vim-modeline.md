---
id: 150
title: モードライン
date: 2009-02-07T09:15:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/02/07/%e3%83%a2%e3%83%bc%e3%83%89%e3%83%a9%e3%82%a4%e3%83%b3/'
permalink: /2009/02/07/vim-modeline/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/02/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7073728056396634468
categories:
  - コンピュータ
tags:
  - vim
---
Portfileの最初の行におまじないのような一行がある．
<pre># -*- coding: utf-8; mode: tcl; tab-width: 4; indent-tabs-mode: nil; c-basic-offset: 4 -*- vim:fenc=utf-8:ft=tcl:et:sw=4:ts=4:sts=4</pre>
EmacsとVim用にソースの種類やタブの取り扱いを設定するためのもので，モードラインと
呼ばれている．

Portfileの書き方として推奨されているので，よく考えずにこの行をつけていた．

モードラインの設定に従うはずなのに，この行があるにもかかわらず，~/.vimrcの設定が使われるので，モードラインが有効になっていないことに気づいた．

モードラインを有効にするには，
<pre>set modeline
set modelines=1</pre>
とする．いつも使うのなら，~/.vimrcに書いておけば良い．モードラインはset modelineで有効になる．モードラインの設定を検索する行数は，set modelinesで指定する．既定では，モードラインは無効でmodelines=0のようであるので，モードラインを使うにはこの設定が必要である．

後半にあるvimの部分では，テキストのエンコーディングをutf-8に（fenc=utf-8），ファイルタイプをtclに（ft=tcl），タブを展開（et），インデント，タブ，ソフトタブをそれぞれ4文字に設定している．ソフトタブに0でない値を設定すると，タブを入力したとき設定した文字数の空白に置換する．

ソースの種類により，スタイルは異なっている．Makefileはタブが必要なので，いつもタブの展開（set expandtab）しておくわけにはいかない．Cなど通常のソースでは，タブが4つの空白にすることが推奨されることが多い．長い数式を書き，doループが多重になることが多いFortranのソースでは，タブは2つくらいにしておきたい．このような場合でも<span style="text-decoration: underline;"><span style="font-weight: bold;"><span style="font-weight: bold;">，</span></span></span>ソースの最初にモードラインを書いておけば，様々なスタイルに対応することができる．

Portfileは拡張子がないが，モードラインの設定のおかげで，文法に基づいた色づけ（syntax enable）を~/.vimrc等に設定しておけば，キーワード等に色がつく．インデント等の設定があるために，文字を揃えるのが容易になった．大変便利だ．Fortranやnclのソースにも適宜モードラインを設定して，見やすいソースを書くようにしたい．