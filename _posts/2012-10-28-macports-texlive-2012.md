---
id: 47
title: MacPortsでTeXLive 2012をインストール
date: 2012-10-28T18:01:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/10/28/macports%e3%81%a7texlive-2012%e3%82%92%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2012/10/28/macports-texlive-2012/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/10/macportstexlive-2012.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7083436565453124286
categories:
  - コンピュータ
tags:
  - macports
  - TeX
---
ずっとMacPortsでptexを使ってきた． <!--more-->

<a href="https://svn.macports.org/repository/macports/trunk/dports/tex/blahtexml/Portfile">blahtexml</a>のPortfileを書いているときに，manual.pdfの生成にucs.styが必要となった．ちょっと調べてみると，texlive-latex-extraに入ってることが分かった．MacPortsのTeXLiveパッケージの中身は，この<a href="http://trac.macports.org/wiki/TeXLivePackages">ページ</a>にまとめられている。ついでにTeXLive 2011でptexが含まれるようになったことが分かった．
<pre>$ sudo port -d install texlive-lang-cjk</pre>
とするとtexlive一式とtexlive-lang-cjkがインストールされ，platexで日本語が扱える．さらに，uptexも入っている．テストとしてhello.texを準備し，
<pre></pre>
<pre>$ platex hello
$ dvipdfmx hello</pre>
とするとhello.pdfが生成される．ただし，ヒラギノは埋め込まれない． ptex同様にヒラギノを埋め込むようにする．TexLiveでは，カスタマイズは${prefix}/share/texmf-local以下にするのが流儀だそうだ．<a href="http://www.fugenji.org/~thomas/texlive-guide/font_setup.html">ここ</a>を参考に以下のようにする．
<ol>
 	<li>ヒラギノのシンボリックリンクを作成．</li>
 	<li>データベース更新 (mktexlsr)</li>
 	<li>フォントマップの選択</li>
</ol>
<pre>$ sudo mkdir -p /opt/local/share/texmf-local/fonts/opentype/public/hiragino/
$ cd /opt/local/share/texmf-local/fonts/opentype/public/hiragino/
$ sudo ln -fs "/Library/Fonts/ヒラギノ明朝 Pro W3.otf" ./HiraMinPro-W3.otf 
$ sudo ln -fs "/Library/Fonts/ヒラギノ明朝 Pro W6.otf" ./HiraMinPro-W6.otf
$ sudo ln -fs "/Library/Fonts/ヒラギノ丸ゴ Pro W4.otf" ./HiraMaruPro-W4.otf
$ sudo ln -fs "/Library/Fonts/ヒラギノ角ゴ Pro W3.otf" ./HiraKakuPro-W3.otf
$ sudo ln -fs "/Library/Fonts/ヒラギノ角ゴ Pro W6.otf" ./HiraKakuPro-W6.otf
$ sudo ln -fs "/Library/Fonts/ヒラギノ角ゴ Std W8.otf" ./HiraKakuStd-W8.otf
$ sudo mktexlsr
$ sudo updmap-setup-kanji hiragino</pre>
フォントが埋め込まれているかどうかは，pdffontsというコマンドで確認できる．
<pre>$ pdffonts hello.pdf</pre>