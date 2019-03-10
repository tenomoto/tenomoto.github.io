---
id: 81
title: zencoding.vim
date: 2010-12-05T17:33:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2010/12/05/zencoding-vim/
permalink: /2010/12/05/zencoding-vim/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/12/zencodingvim.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8349749600987822011
categories:
  - コンピュータ
tags:
  - vim
---
HTMLやCSSを手早く書くためのvimスクリプト<a href="http://mattn.kaoriya.net/software/vim/20100306021632.htm">zencoding.vim</a><br /><br />~/.vim/bundleに<a href="https://github.com/tpope/vim-pathogen">pathogen</a>をclone.<br /><br />~/.vim/autoload/にautoload/pathogen.vimのリンクを張る.<br /><br />.vimrcの設定.<br /><pre><br />call pathogen#runtime_append_all_bundles()<br />call pathogen#helptags()<br /></pre>