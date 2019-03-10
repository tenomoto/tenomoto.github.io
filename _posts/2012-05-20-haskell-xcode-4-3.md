---
id: 55
title: HaskellとXcode 4.3
date: 2012-05-20T02:40:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/05/20/haskell%e3%81%a8xcode-4-3/'
permalink: /2012/05/20/haskell-xcode-4-3/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/05/haskellxcode-43.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5300435978639692152
categories:
  - コンピュータ
tags:
  - Haskell
  - Mac
---
Haskell-platform 2011.4をインストールした．<!--more-->

パッケージをインストール途中，ghcが/Developer/usr/bin/gccがないと言って止まる．/usr/bin/ghcはシェルスクリプトで，ここにgccへのパスが書いてある．Xcode-4.3からXcodeはただのアプリケーションになったので，/Developerは/Applications/Xcode.app/Contents/Developerに移動．でも長ったらしいので，/usr/bin/gccとしておいた．/usr/bin/clangにしてみたが，コンパイルはうまくいかない．なお，/usr/bin/ghcはシンボリックリンク．