---
id: 80
title: Octaveで2Dグラフ
date: 2010-12-17T09:59:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/12/17/octave%e3%81%a72d%e3%82%b0%e3%83%a9%e3%83%95/'
permalink: /2010/12/17/octave-2d-plot/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/12/octave2d.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8612219688438352668
categories:
  - コンピュータ
tags:
  - macports
  - Octave
---
Octaveの<a href="http://www.gnu.org/software/octave/doc/interpreter/Two_002dDimensional-Plots.html#Two_002dDimensional-Plots">マニュアル</a>などの入門では, sinのような組込函数を描く例が多い.

描きたいのはsinではない. 論文に出てきた式を図にして確認したい.

例として描いてみるのは, CALIPSO搭載CALIOPセンサを使って見積もられた過冷却水の気温に対する依存性 (<a href="http://dx.doi.org/10.1029/2009JD012384">Hu et al. 2010</a>のFig. 6dの赤い線) である.

pやfを函数定義 (function endfunction) してもよいが, ここでは単にx軸に対応する値を計算するにとどめる.

tの階乗は要素毎なので, スカラの階乗**に.をつけて.**とする. %のあとの文字はコメントである.

MacPortsでインストールしたばあい, AquaTermがデフォルトなので, 描かれた図はPDFかEPSで保存できる.
<pre>
t = -40:0.1:0; % -40°Cから0°Cまで0.1°C刻み
p = 7.6725 + 1.0118*t + 0.1422*t.**2 + 0.0106*t.**3 + 3.39e-4*t.**4 +3.95e-6*t.**5; % 式(4)
f = 1./(1+exp(-p)); % 式(1)
plot(t,f)</pre>