---
id: 143
title: VTK形式のファイルを描画
date: 2009-03-08T22:12:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/08/vtk%e5%bd%a2%e5%bc%8f%e3%81%ae%e3%83%95%e3%82%a1%e3%82%a4%e3%83%ab%e3%82%92%e6%8f%8f%e7%94%bb/'
permalink: /2009/03/08/draw-vtk-format/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/vtk.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3794951752912211027
categories:
  - コンピュータ
tags:
  - VTK
---
vtkinteractionを使う一部のサンプルでBus errorやSegmentation Faultが出る．VTK-5.2.1に更新したがだめだった．仕方がないので，単に表示してしばらくしたら終了するようにした．仮に動作しても，表示はParaViewの方がおそらく便利．

<pre>
#!/bin/sh
# ¥
exec vtk "$0" ${1+"$@"}
package require vtk

if {$argc&lt;1} {
    puts stderr "vtk draw.tcl filename"
    exit
}

vtkPolyDataReader reader
    reader SetFileName [lindex $argv 0]

vtkPolyDataMapper sphereMapper
    sphereMapper SetInputConnection [reader GetOutputPort]
    reader Delete

vtkActor sphereActor
    sphereActor SetMapper sphereMapper

vtkRenderer ren1
    ren1 AddActor sphereActor

vtkRenderWindow renWin
    renWin AddRenderer ren1
    renWin SetSize 300 300
    renWin Render

after 1000

vtkCommand DeleteAllObjects</pre>