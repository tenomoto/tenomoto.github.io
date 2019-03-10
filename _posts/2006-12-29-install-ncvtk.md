---
id: 235
title: Ncvtkのインストール
date: 2006-12-29T17:36:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2006/12/29/ncvtk%e3%81%ae%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2006/12/29/install-ncvtk/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2006/12/ncvtk_29.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3721321393125847642
categories:
  - コンピュータ
tags:
  - NetCDF
  - VTK
---
<div>

Mac OS X上で、X11ではなく、Aquaを使ったVTKを構築し、Ncvtkをインストールしてみよう。
<h3>1. <a href="http://www.cmake.org/">cmake</a>, <a href="http://www.g95.org/">g95</a> (オプション）, <a href="http://www.unidata.ucar.edu/software/udunits/">udunits</a>, <a href="http://www.unidata.ucar.edu/software/netcdf/">netCDF</a></h3>
<blockquote>sudo port install cmake
sudo port install g95
sudo port install netcdf +g95 # このサイトのportfileを利用
sudo port install udunits # このサイトのportfileを利用</blockquote>
<h3>2. <a href="http://www.tcl.tk/">Tcl/Tk</a></h3>
<blockquote>make -C tcl8.4.14/macosx
sudo make -C tcl8.4.14/macosx install
make -C tk8.4.14/macosx
sudo make -C tk8.4.14/macosx install</blockquote>
<h3>3. <a href="http://www.python.org/">Python</a></h3>
<blockquote>./configure –enable-framework
make
sudo make install
cd /usr/local
sudo ln -s /Library/Frameworks/Python.framework/Versions/¥
Current/lib/python2.5 .</blockquote>
<h3>4. <a href="http://numpy.sourceforge.net/">Numeric, , </a><a href="http://starship.python.net/~hinsen/ScientificPython/">ScientificPython</a></h3>
Numeric, ScientificPythonの順に
<blockquote>python setup.py build &amp;&amp; sudo python setup.py install</blockquote>
を実行してインストール.
<h3>5. <a href="http://pmw.sourceforge.net/">Pmw</a></h3>
<blockquote>cd /Library/Frameworks/Python.framework/Versions/Current/¥
lib/python2.5/site-packages
sudo tar zxvf ~/Pmw-1.2.tar.gz</blockquote>
<h3>6. <a href="http://www.vtk.org/">VTK</a></h3>
CVSからVTK 5.xを取得．VTKというディレクトリができる.
<blockquote>mkdir build
cd build
cmake -DBUILD_EXAMPLES=ON -DBUILD_SHARED_LIBS=ON -DVTK_USE_CARBON=ON -DVTK_WRAP_TCL=ON -DVTK_WRAP_PYTHON=ON -DPYTHON_EXECUTABLE=/usr/local/bin/python ../VTK
ccmake ../VTK
make
sudo make install</blockquote>
<h3>7. Ncvtk</h3>
<blockquote>python setup.py build &amp;&amp; sudo python setup.py install</blockquote>
バイナリは
<code>/Library/Frameworks/Python.framework/Versions/Current/bin</code>

にできるので，適当なところ，例えば/usr/local/binにシンボリック・リンクをはるか, 上記ディレクトリにバスを通しておく．
<code>ciaworld.nc</code>は, <code>site-packages/ncvtk/data</code>にインストール.

</div>