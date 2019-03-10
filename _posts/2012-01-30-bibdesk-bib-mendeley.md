---
id: 63
title: BibDeskのbibファイルをMendeleyに取り込む
date: 2012-01-30T14:08:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/01/30/bibdesk%e3%81%aebib%e3%83%95%e3%82%a1%e3%82%a4%e3%83%ab%e3%82%92mendeley%e3%81%ab%e5%8f%96%e3%82%8a%e8%be%bc%e3%82%80/'
permalink: /2012/01/30/bibdesk-bib-mendeley/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/01/bibdeskbibmendeley.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1595624840833297383
categories:
  - コンピュータ
tags:
  - Mendeley
  - TeX
---
Mendeleyはクラウド対応の文献管理アプリケーション。Wordでの引用、文献リスト作成にはMendeleyが便利。
ToolsメニューからInstall Word pluginを実行するとAppleScriptがインストールされる
引用箇所でCommand+Control+iを叩いて引用を作成。文献リスト作成箇所ではCommand+Control+b。
PDFから適宜データを取り込んでくれるというふれこみだが、うまくいかなかった。不完全なデータの手直しは不便に感じられた。
試しに、BibDeskのbibファイルをDrag&amp;DropでMedeleyに取り込んでみる。省略記号（例:MWR）で記入していたjournal名が落ちていた。定義をbibファイルの冒頭に書いてあるものは、置き換えられる。Mendeleyでは、journal名の略記（例: Mon. Wea. Rev.）中の 、title中の{}が不要である。そのまま取り込むとや{}が残ってしまう。そこで、Mendeleyの取り込みに適した形にbibファイルを加工した。加工内容は
<ol>
 	<li>Journalの定義とデータベースを結合</li>
 	<li>Journal名の略記中のを削除</li>
 	<li>Title中の{}を削除</li>
</ol>
である。3はTitle = {を[に},を]に一旦置き換えて{}を削除し、[,]をそれぞれTitle =と},に戻している。
bibdesk2mendeley.sh
<pre>#!/bin/sh
bibdir="${HOME}/Documents/Bibdesk/bib"
abb=$bibdir/ametsoc.bib
ref=$bibdir/references.bib
tmp=./tmp.bib
cat $abb $ref &gt; $tmp
sed -e 's/\ / /g; s/Title = {/[/; s/},/]/' $tmp | 
awk '/^[ t]*[/{gsub(/{/,""); gsub(/}/,""); print}; !/^[ t]*[/{print}' | 
sed -e 's/[/Title = {/;s/]/},/'
rm -f $tmp</pre>