---
id: 170
title: Octaveで簡易ベンチマーク
date: 2008-09-21T09:39:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/09/21/octave%e3%81%a7%e7%b0%a1%e6%98%93%e3%83%99%e3%83%b3%e3%83%81%e3%83%9e%e3%83%bc%e3%82%af/'
permalink: /2008/09/21/octave-simple-benchmark/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/04/octave.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/8373057278364992078
categories:
  - コンピュータ
tags:
  - Mac
  - Octave
---
MATLABを使った精度保証付き演算を紹介している荻田さんの<a href="http://lab.twcu.ac.jp/ogita/math/matlab/smpmatlab.htm">ページ</a>にある方法
<pre> n=2000; A=randn(n); B=randn(n);
tic; C=A*B; t=toc, MFLOPS=2*n^3/t*1e-6</pre>
でMacの演算性能を測ってみた．MATLABは持っていないので，<a href="http://www.macports.org/">MacPorts</a>でインストールした<a href="http://www.octave.org/">Octave</a> (octave @2.9.15_0+g95+ptex+test)を用いた．
<ul>
 	<li>Mac mini (PowerPC G4 1.25 GHz): 約 1 Gflops</li>
 	<li>MacBook (Core Duo 1.83 GHz): 約 3 Gflops</li>
 	<li>iMac G5 (PowePC 1.9 GHz): 約 4 Gflops</li>
 	<li>PowerMac G5 (PowerPC G5 Dual 2.7 GHz): 約 10 Gflops</li>
 	<li>iMac (Core 2 Duo 2.4 GHz): 約 12.5 Gflops</li>
 	<li>Mac Pro (Xeon 3 GHz クアッドコア×2): 約 50 Gflops</li>
 	<li>ASUS V3-M2V690G (Athlon 64 X2 5400+, Ubuntu 8.0.4): 約0.7Gflops, 約3.5flops (ATLAS), 約5Gflops (ACML)</li>
</ul>
g95はOpenMPに対応していないが，アクティビティモニタを見るとCPUは二つとも動いているので，スレッド化されているようだ．おそらく，Mac OS XのAccelerate.frameworkに含まれているBLAS/LAPACKが呼ばれていて，Fortranコンパイラは無関係だと思われる．

PowerPC G5がXeon 3.06 GHzの1コアに遜色ない性能を出したのはちょっとうれしい．

Core 2 DuoのiMacも侮れない... iMac Early 2008 (Core 2 Duo 3.06 GHz) では, 15 Gflops出るだろうか.
<div>
<div></div>
<div>Mac Proは, 地球シミュレータ1ノードの理論値64 Gflopsまであと少し．でもIntelの<a href="http://www.intel.co.jp/jp/performance/server/xeon/hpcapp.htm">データ</a>からすると、限界まで出せてなさそう。

UbuntuのoctaveはAMD64には最適化されているようだが, ATLASもACMLもなしだと, Mac miniより遅かった. Mac OS XのAccelerate.frameworkはありがたい.</div>
</div>