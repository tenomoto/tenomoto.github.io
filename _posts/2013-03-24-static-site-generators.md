---
id: 40
title: 静的サイト生成ツールの導入
date: 2013-03-24T06:36:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2013/03/24/%e9%9d%99%e7%9a%84%e3%82%b5%e3%82%a4%e3%83%88%e7%94%9f%e6%88%90%e3%83%84%e3%83%bc%e3%83%ab%e3%81%ae%e5%b0%8e%e5%85%a5/'
permalink: /2013/03/24/static-site-generators/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2013/03/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3566815920082018740
categories:
  - コンピュータ
tags:
  - blosxom
  - Hakyll
  - Haskell
  - Hyde
  - Jekyll
  - Markdown
  - python
  - Ruby
  - static site generator
---
静的ウェブサイトは，あらかじめウェブページをHTMLページを作っておいたサイトを言う．動的サイトをスクリプト言語とすると，静的サイトはコンパイル言語に対応する．<!--more-->

現在では，PHPなどを使った動的ウェブサイトが一般的になっていて，静的サイトは古いと考えられている．しかし，速度やセキュリティの面で静的サイトにも利点がある．静的サイトを選択した場合，HTMLを手で書いていたのでは手間がかかる．

そこで，<a href="http://daringfireball.net/projects/markdown/">markdown</a>記法などで入力となるテキストファイルを用意し，これを処理してサイトを生成する静的サイト生成ツール（static site generator）が考案された．入力となるテキストファイルには，タイトルやメタ情報をタグとして記述できる．コンパイル言語でMakeやCMakeを使ってバイナリを生成するのに似ている．

以前は，<a href="http://blosxom.sourceforge.net/">bloxsom</a>を使ってサイトを作っていた．bloxsomのプラグインとして<a href="http://daringfireball.net/projects/downloads/Markdown_1.0.1.zip">markdown.pl</a>を使い，markdownからHTMLを生成させていた．プロジェクト管理にはMakeを使った．

最近は，便利な静的サイト生成ツールがいくつもある．
<ul>
 	<li>Rubyで書かれた<a href="http://jekyllrb.com/">Jekyll</a></li>
 	<li>Pythonで書かれた<a href="http://hyde.github.com/">Hyde</a></li>
 	<li>Haskellで書かれた<a href="http://jaspervdj.be/hakyll/">Hakyll</a></li>
</ul>
これらをOS X Mountain Lion 10.8.3 に導入してみた．普段は何でもMacPortsで入れるのだが，ここではRuby, Python, Haskellそれぞれの独自のパッケージ管理システムを利用する．
<h3>Jekyllの導入</h3>
<pre>sudo gem update --system
sudo gem install jekyll</pre>
<h3>Hydeの導入</h3>
<pre>sudo easy_install pip
sudo pip install hyde</pre>
typogrify-hydeの導入に失敗する．<a href="https://github.com/hyde/hyde/pull/193">これを先にインストールする</a>とうまくいく．
<pre>sudo pip install git+git://github.com/hyde/typogrify.git#egg=typogrify-hyde
sudo pip install hyde</pre>
<h3>Hakyllのインストール</h3>
<a href="http://www.haskell.org/platform/mac.html">Haskel Platform</a>をインストール．私の場合は，古いバージョンがインストールされていたので削除．
<pre>uninstall-hs
uninstall-hs thru 7.4.1
sudo uninstall-hs thru 7.4.1 --remove</pre>
Haskellのパッケージ管理はcabal．データベースを更新してhakyllを導入．
<pre>cabal update
cabal install cabal-install # 
cabal install hakyll</pre>