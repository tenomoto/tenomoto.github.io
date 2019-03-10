---
id: 231
title: Ncvtkを使ってみる
date: 2006-12-31T16:29:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2006/12/31/ncvtk%e3%82%92%e4%bd%bf%e3%81%a3%e3%81%a6%e3%81%bf%e3%82%8b/'
permalink: /2006/12/31/how-to-use-ncvtk/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2006/12/ncvtk.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/5711065229981222512
image: /wp-content/uploads/2006/12/ncvtk_carbon-672x372.png
categories:
  - コンピュータ
tags:
  - NetCDF
  - VTK
---
Ncvtkを実際に使って、画像やムービーを作成してみる。

<a href="/wp-content/uploads/2006/12/ncvtk_carbon.png"><img id="BLOGGER_PHOTO_ID_5282839820657730210" style="float: left; margin: 0 10px 10px 0; cursor: hand; width: 200px; height: 150px;" src="/wp-content/uploads/2006/12/ncvtk_carbon-300x225.png" alt="" border="0" /></a>
<ul>
 	<li>ターミナルでncvtk2と打つと起動する．</li>
 	<li>可視化できるのはCDCの規約に準拠したnetCDFである．</li>
 	<li>起動時に-fオプションでファイル名を指定するか，起動後メニューからOpenを選ぶ．</li>
 	<li>鉛直座標軸が認識されないときは，-z (–elev) オプションで指定（正規表現可）．</li>
 	<li>その他オプションは-h (–help)で調べる．</li>
 	<li>開いたファイルは，Macのメニューバーに隠れてしまう．一度Render WindowをDockにしまってもとに戻すと，開いたファイルのウインドウが現れる．</li>
 	<li>ファイルのウインドウを選択して，Visualizeメニューから可視化方法を選択する．</li>
 	<li>マウスで球を回転できる．Aquaの場合，Ctrl+Shiftを押しながらだとズーム，Shiftだと移動，Ctrlだと水平の回転．</li>
</ul>