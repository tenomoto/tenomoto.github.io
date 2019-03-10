---
id: 282
title: 理想の ANSI Color を作ってみる
date: 2013-05-29T00:27:33+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2013/05/29/an-engineers-log-ansi-color/
permalink: /2013/05/29/an-engineers-log-ansi-color/
tumblr_hiyokoz_permalink:
  - http://hiyokoz.tumblr.com/post/51601238523/an-engineers-log-ansi-color
tumblr_hiyokoz_id:
  - "51601238523"
categories:
  - コンピュータ
tags:
  - Terminal
format: link
---
[An Engineer's Log: 理想の ANSI Color を作ってみる](http://anengineer.tumblr.com/post/25024241014/ansi-color)
<!--more-->

<blockquote>
<p>どうも生の ANSI Color の配色って見にくいので、
<a href="http://www.yafla.com/yaflaColor/ColorRGBHSL.aspx">yaflaColor - Simple Web Color Utility And RGB/HSV Conversion</a>
を使って HSV モデルに基づいた配色を行う。</p> <p>方針は下の通り。</p> <ul><li>白と黒は <ul><li>当然 Saturation(彩度) 0&#160;%</li>
<li>白の Value(輝度) は 80%、黒の Value は 0% でボールドは 20%増し</li>
</ul></li>
<li>白と黒以外 <ul><li>Hue(色相) は60 Degrees 単位 <ul><li>赤は 0</li>
<li>黄色は 60</li>
<li>緑は 120</li>
<li>シアンは 180</li>
<li>青は 240</li>
<li>マゼンダは 300</li>
</ul></li>
<li>&#8230;</li></ul></li></ul></blockquote></div>