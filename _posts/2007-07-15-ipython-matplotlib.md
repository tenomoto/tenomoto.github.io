---
id: 205
title: ipythonとmatplotlib
date: 2007-07-15T19:44:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2007/07/15/ipython%e3%81%a8matplotlib/'
permalink: /2007/07/15/ipython-matplotlib/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2007/07/ipythonmatplotlib.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6384531436165675566
categories:
  - コンピュータ
tags:
  - python
---
<div>

<a href="http://ipython.scipy.org/">ipython</a>は, インタラクティブ機能を強化したpythonのシェル. <a href="http://matplotlib.sourceforge.net/">matplotlib</a>は, pythonから使えるMATLAB互換の2次元プロットライブラリ.

地図投影して等値線も描けるようなので, MacPortsを使ってインストールしてみた. py-dateutilとpy-scientificはPortfileを書き換えて新しいバージョン (python-dateutil-1.2とScientific-2.6) を使った.

GTK+は重そうなので, wxWidgetsにした. TkinterではBus errorが出たが, 初期設定をきちんとしていなかったからかもしれない.

数値配列は, numpyにした. 最初はnumarrayにしたが, depreatedだと警告がでた.

結局, matplotlibで指定したvariantsは, +wxpython +numpyである.

使う前に~/.matplotlib/matplotlibrcを編集し, 使用するGUI (backend) と配列ライブラリ (numerix) を指定する. backendを指定しないと, ウィンドウが表示されない.
<blockquote>backend : wxAgg
numerix : numpy</blockquote>
ipythonには, variantsはない.

<a href="http://matplotlib.sourceforge.net/matplotlib.pylab.html">pylab</a>が MATLAB互換モジュールである. MATLABを使ったことがないので, どの程度の互換性があるのかはよく分からない. ipythonの起動オプションで, -pylabを指定するとmatplotlibの設定が行われるので, 直ちにpylabモジュールが使えるようになる.

<a href="http://matplotlib.sourceforge.net/users/pyplot_tutorial.html">チュートリアル</a>を試してみるといいだろう. ただし, ipython -pylabとすればimport pylab *やshow()は不要である.
描画ウインドウを出すコマンドはfigure(), 中身を消すのはclf(), 閉じるのはclose()である.

</div>