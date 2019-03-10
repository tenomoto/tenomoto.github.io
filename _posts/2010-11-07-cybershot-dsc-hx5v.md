---
id: 83
title: Cybershot DSC-HX5V
date: 2010-11-07T11:29:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2010/11/07/cybershot-dsc-hx5v/
permalink: /2010/11/07/cybershot-dsc-hx5v/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/11/cybershot-dsc-hx5v.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/2456415985932561880
categories:
  - デジカメ
tags:
  - Cybershot
  - GPS
  - Mac
---
SONYのGPS付デジカメ<a href="http://www.amazon.co.jp/gp/product/B0038OLMF2?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=B0038OLMF2">DSC-HX5V</a>を購入.<br /><br />位置取得時間を短縮するために，GPSアシストデータを更新する必要がある. マニュアルによると, カメラを専用ケーブルでPCにつなぎ, Windows版しかないPMBから更新することになっている.<br /><br />Kakaku.comのクチコミ掲示板にメモリカードの所定の場所にファイルを保存しているだけだとあったので, シェルスクリプトを作成した. このスクリプトを使えば, 専用ケーブルもWindows PCも不要だ. 引数にはカードの名前を指定する. <a href="http://www.amazon.co.jp/gp/product/B0038OLMF2?ie=UTF8&amp;tag=enomospheddoj-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=B0038OLMF2">DSC-HX5V</a>はメモリースティックだけでなく, SDカードも使える. 最近の<a href="http://www.amazon.co.jp/gp/redirect.html?ie=UTF8&amp;location=http%3A%2F%2Fwww.amazon.co.jp%2Fs%3Fie%3DUTF8%26redirect%3Dtrue%26ref_%3Dsr_nr_n_1%26keywords%3DMacBook%26bbn%3D164353011%26qid%3D1289097452%26rnid%3D164353011%26rh%3Dn%253A3210981%252Cn%253A%25213211011%252Cn%253A%252110667061%252Cn%253A%2521404949011%252Cn%253A13447861%252Cn%253A164353011%252Ck%253AMacBook%252Cn%253A84178051&amp;tag=enomospheddoj-22&amp;linkCode=ur2&amp;camp=247&amp;creative=7399">MacBook Pro</a>には, SDカードスロットがあるので, カードリーダもいらない.<br /><br /><pre><br />#!/bin/sh<br />URL=http://control.d-imaging.sony.co.jp/GPS/assistme.dat<br />CURL=/usr/bin/curl<br />CURLOPTS="--create-dirs -o"<br />if [ $# -lt 1 ]; then<br />  echo "Usage:: $0 Volume"<br />  exit<br />fi<br />VOL=$1<br />OUT=/Volumes/$VOL/PRIVATE/SONY/GPS/ASSISTME.DAT<br />$CURL $CURLOPTS "$OUT" $URL<br /></pre>