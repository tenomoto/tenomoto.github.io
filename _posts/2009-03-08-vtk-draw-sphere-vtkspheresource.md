---
id: 144
title: VTKで球を描く (vtkSphereSource)
date: 2009-03-08T22:07:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/08/vtk%e3%81%a7%e7%90%83%e3%82%92%e6%8f%8f%e3%81%8f-vtkspheresource/'
permalink: /2009/03/08/vtk-draw-sphere-vtkspheresource/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/vtk-vtkspheresource.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1882937809558767950
categories:
  - コンピュータ
tags:
  - VTK
---
MacPortsでvtk5をインストール．デフォルトは，Cocoa．X11ではコンパイルに失敗した．まずは，お手軽にTclで球を描いてファイルに保存．次のスクリプトを適当な名前（例えばsphere1.tcl）で保存して，実行（vtk sphere1.tcl）．
<pre>
package require vtk

vtkSphereSource sphere
        sphere SetRadius 1.0
        sphere SetPhiResolution 100
        sphere SetThetaResolution 50

vtkPolyDataWriter writer
        writer SetInput [sphere GetOutput]
        writer SetFileName sphere1.vtk
        writer Write

sphere Delete
writer Delete</pre>