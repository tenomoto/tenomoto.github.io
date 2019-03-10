---
id: 44
title: texlive-lang-cjk導入時のTeXShopの設定
date: 2013-01-08T14:07:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2013/01/08/texlive-lang-cjk%e5%b0%8e%e5%85%a5%e6%99%82%e3%81%aetexshop%e3%81%ae%e8%a8%ad%e5%ae%9a/'
permalink: /2013/01/08/texlive-lang-cjk-texshop-config/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2013/01/texlive-lang-cjktexshop.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5766610153950156918
categories:
  - コンピュータ
tags:
  - macports
  - TeX
  - TeXShop
---
奥村先生の<a href="http://oku.edu.mie-u.ac.jp/~okumura/texwiki/?TeXShop">ページ</a>に書いてありますが，シンボリックリンクを使って少し手抜き。<!--more-->

pdfplatexだけを使う場合は最初のシェルスクリプトだけでもよい。
<pre>$ cd ~/Library/TeXShop/bin
$ cat pdfeptex
#!/bin/sh
command=`basename ${0}`
${command#pdf} -synctex=1 "$1" &amp;&amp; 
dvipdfmx "`basename "$1" .tex`"

$ ln -s pdfeptex pdfplatex
$ ln -s pdfeptex pdfeuptex
$ ln -s pdfeptex pdfuplatex

$ cat pdfeptex2
#!/bin/sh
command2=`basename ${0}`
command=${command2#pdf}
${command%2} -synctex=1 "$1" &amp;&amp; 
dvips -Ppdf -z -f "`basename "$1" .tex`.dvi" | 
convbkmk -g &gt; "`basename "$1" .tex`.ps" &amp;&amp; 
ps2pdf "`basename "$1" .tex`.ps"

$ ln -s pdfeptex2 pdfplatex2
$ ln -s pdfeptex2 pdfeuptex2
$ ln -s pdfeptex2 pdfuplatex2

$ cat eptex2pdf-utf8
#!/bin/sh
# iNoue Koich! (modified by S. Zenitani)

export PATH=$PATH:/usr/texbin:/usr/local/bin

COMMAND=${0##*/}
PTEX=${COMMAND%2pdf-*}
ENCODE=${COMMAND#*-}
JOBNAME=${1##*/}
JOBNAME=${JOBNAME%.*}

eptex -synctex=1 -kanji=$ENCODE -progname=$PTEX $1 &amp;&amp; 
dvipdfmx $JOBNAME

$ ln -s eptex2pdf-utf8 platex2pdf-utf8
$ ln -s eptex2pdf-utf8 euptex2pdf-utf8
$ ln -s eptex2pdf-utf8 uplatex2pdf-utf8</pre>