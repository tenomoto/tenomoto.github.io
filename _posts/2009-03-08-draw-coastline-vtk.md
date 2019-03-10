---
id: 141
title: VTKで地球を描く
date: 2009-03-08T22:33:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/08/%e5%9c%b0%e7%90%83%e3%82%92%e6%8f%8f%e3%81%8f/'
permalink: /2009/03/08/draw-coastline-vtk/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7778855364552281061
categories:
  - コンピュータ
tags:
  - VTK
---
vtkEarthSourceで海岸線付きの球が描ける．SetOnRatioの既定は10で1が一番細かい．日本の形状は少しまともになるが，北海道，四国，九州が出てこない...
<pre>
package require vtk

vtkEarthSource earth
    earth SetOnRatio 1

vtkPolyDataWriter writer
    writer SetInput [earth GetOutput]
    writer SetFileName earth.vtk
    writer Write

writer Delete
earth Delete</pre>