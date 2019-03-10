---
id: 76
title: VimでFortranのsyntax colouring
date: 2011-01-06T16:39:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2011/01/06/vim%e3%81%a7fortran%e3%81%aesyntax-colouring/'
permalink: /2011/01/06/vim-fortran-syntax-colouring/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2011/01/vimfortransyntax-colouring.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2670708867588879049
categories:
  - コンピュータ
tags:
  - Fortran
  - vim
---
このところsyntax colouringを使ってきたが，拡張子がf90なのに固定形式として認識されているようだった．
調べてみると，先頭250行を見て判断していることが分かった．
このソースは，左端から6桁開いているが，72桁より長いところが
無効としてハイライトされていた．

拡張子がfとFの時に固定形式とするには，.vimrcに次のように書く．
filetype plugin indent onはsyntax onよりも前でなくてはならない．

なお，既定では，新しいファイルは固定形式と仮定するようだ．
これまでは，少し書いてから，いったん保存して開き直していた．
<pre>
filetype plugin indent on
let s:extfname = expand("%:e")
if s:extfname ==? "f" || s:extfname ==? "F"
    let fortran_fixed_source=1
    unlet! fortran_free_source
else
    let fortran_free_source=1
    unlet! fortran_fixed_source
endif
syntax on
autocmd FileType * set formatoptions-=tcq</pre>
最後の行は，自動改行を防ぐ<a href="http://vimwiki.net/?faq%2F9">おまじない</a>．