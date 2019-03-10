---
id: 271
title: Durran and Klemp (1983)の山
date: 2013-09-20T03:39:36+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2013/09/20/durran-and-klemp-1983/
permalink: /2013/09/20/durran-and-klemp-1983/
tumblr_hiyokoz_permalink:
  - http://hiyokoz.tumblr.com/post/61731238914/durran-and-klemp-1983
tumblr_hiyokoz_id:
  - "61731238914"
categories:
  - 研究
tags:
  - PSTricks
---
今時は<a href="http://www.texample.net">TikZ</a>を使うべきなのかもしれないが，慣れているPStricksで作成。<!--more-->

<img src="http://media.tumblr.com/bd8d57903d23342f27b4bf359042177b/tumblr_inline_mtenf1kePi1s0tikq.png" alt="" />

<code>readtata</code>で読んで<code>dataplot</code>で描くデータはOctaveで作ったが，何を使っても構わない。形式は，<code>(x1, y1) (x2, y2), ...</code>。
<pre><code>documentclass{article}

usepackage{pstricks}
usepackage{pst-eps}
usepackage{pst-plot}

begin{document}
TeXtoEPS
psset{xunit=40mm, yunit=20mm}
pspicture(-2,0)(2,2.5)
readdata{mydata}{mountain.data}
dataplot[linewidth=2.0pt,plotstyle=curve]{mydata}
rput(-0.15,2){$h_0$}
rput(-0.35,1){$h_0/2$}
rput(-0.12,0.6){$a$}
rput(0.12,0.6){$a$}
rput(0.,-0.1){$x_0$}
rput(0.7,0.8){$displaystyle z=frac{h_0}{1+(x-x_mathrm{0})^2/a^2}$}
psaxes[linewidth=1.2pt,ticks=none,labels=none]{-&gt;}(0,0)(-1.5,0)(1.5,2.2)
psline(-0.2,1)(0.2,1)
psline{&lt;-&gt;}(-0.2,0.5)(0.0,0.5)
psline{&lt;-&gt;}(0.0,0.5)(0.2,0.5)
psline[linestyle=dotted](-0.2,0)(-0.2,1)
psline[linestyle=dotted](0.2,0)(0.2,1)
endpspicture
endTeXtoEPS

end{document}
</code></pre>