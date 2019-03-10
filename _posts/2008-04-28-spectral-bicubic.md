---
id: 183
title: スペクトル微係数を用いた双3次空間内挿法
date: 2008-04-28T18:47:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/04/28/%e3%82%b9%e3%83%9a%e3%82%af%e3%83%88%e3%83%ab%e5%be%ae%e4%bf%82%e6%95%b0%e3%82%92%e7%94%a8%e3%81%84%e3%81%9f%e5%8f%8c3%e6%ac%a1%e7%a9%ba%e9%96%93%e5%86%85%e6%8c%bf%e6%b3%95/'
permalink: /2008/04/28/spectral-bicubic/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/04/3.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7232471143426670330
image: /wp-content/uploads/2008/04/eq_preview-672x372.png
categories:
  - 研究
tags:
  - bicubic
  - legendre
---
<a href="https://www.enomosphere.net/wp-content/uploads/2008/04/eq_preview.png"><img id="BLOGGER_PHOTO_ID_5194235768212276962" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer;" src="https://www.enomosphere.net/wp-content/uploads/2008/04/eq_preview-300x287.png" alt="" border="0" /></a>
多くの数値予報モデルや気候モデルには，時間刻み幅を大きくし，移流を正確に計算するために，セミ・ラグランジュ法が用いられています．オイラー移流と比較して，分散性が少ないが消散があります．空間スケールの小さな構造が減衰して，大気の観測されるスペクトルの表現が困難です．

スペクトルモデルでは，微分が正確に計算できます．このようにして求めた微分係数を双3次内挿法に適用したところ，従来のモデルで用いられてきた双3次ラグランジュ内挿法よりも消散を小さくすることができました．

図は，ガウス型の山を赤道から北極を通りまた赤道に戻るように剛体回転流で20日間で1周させた結果です．黒は初期値, 青はオイラー移流, 赤は双3次ラグランジュ内挿法を用いたセミ・ラグランジュ移流，紫は今回考案した方法です．

この研究について，2008年5月19日 (月)，<a href="http://msj.visitors.jp/notification/pdf/S2008table080404.pdf">日本気象学会春季大会</a>で<a href="http://msj.visitors.jp/notification/pdf/S2008poster080321.pdf">ポスター発表</a> (P225) [<a href="http://sites.google.com/a/enomosphere.net/public/presentations/20080519.pdf?attredirects=0">PDF</a>]しました．