---
id: 142
title: VTKで球を描く (手作り)
date: 2009-03-08T22:16:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/08/vtk%e3%81%a7%e7%90%83%e3%82%92%e6%8f%8f%e3%81%8f-%e6%89%8b%e4%bd%9c%e3%82%8a/'
permalink: /2009/03/08/vtk-draw-sphere-by-hand/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/vtk_08.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/155530980075223721
categories:
  - コンピュータ
tags:
  - VTK
---
vtkSphereSourceは便利だが，勉強にならないので，球をセルから構成してみる．

定数
<pre>package require vtk

set nlon 100
set nlat [expr {$nlon/2 + 1}]
set pi [expr {acos(-1.)}]
set pi2 [expr {$pi * 2.}]
set npts [expr {$nlon * $nlat}]
#puts stdout "pi=$pi pi2=$pi2 npts=$npts"</pre>
経度φと余緯度θからデカルト座標に変換するコマンドを作る．
VTKでは，経度がθ余緯度がφのようだが気にしない．
<pre>proc phitheta2xyz args {
         set phi [lindex $args 0]
         set theta [lindex $args 1]
         set xyz {}
         set sin_theta [expr {sin($theta)}]
   lappend xyz [expr {cos($phi) * $sin_theta}]
   lappend xyz [expr {sin($phi) * $sin_theta}]
         lappend xyz [expr {cos($theta)}]
}</pre>
経度，余緯度を生成．
<pre>set lon {}
set dlon [expr {$pi/$nlon}]
for {set i 0} {$i&lt;$nlon} {incr i} {
    lappend lon [expr {$pi2 * $i / $nlon}]
}
#puts stdout $lon
set lat {}
set dlat [expr {$pi/($nlat-1)}]
for {set j 0} {$j&lt;$nlat} {incr j} {
    lappend lat [expr {$dlat * $j}]
}
#puts stdout $lat</pre>
座標点のデカルト座標を生成してvtkPointsに登録．
<pre>vtkPoints pts
pts SetNumberOfPoints $npts
set i 0
foreach theta $lat {
    foreach phi $lon {
# puts stdout "$phi $theta"
# puts [phitheta2xyz $phi $theta]
      eval pts SetPoint [concat $i [phitheta2xyz $phi $theta]]
      incr i
    }
}</pre>
4点からセルを作る．経度方向に周期境界．$nlon-1番目の隣は，0番目に戻る．
<pre>vtkCellArray clls
set nlonm1 [expr {$nlon - 1}]
for {set j 0} {$j&lt;$nlat-1} {incr j} {
    for {set i 0} {$i&lt;$nlon} {incr i} {
        set k0 [expr {$nlon*$j + $i}]
        if {$i!=$nlonm1} {
            set k1 [expr {$k0 + 1}]
        } else {
            set k1 [expr {$k0 - $nlonm1}]
        }
        set k2 [expr {$k1 + $nlon}]
        set k3 [expr {$k0 + $nlon}]
        clls InsertNextCell 4
        clls InsertCellPoint $k0
        clls InsertCellPoint $k1
        clls InsertCellPoint $k2
        clls InsertCellPoint $k3
    }
}</pre>
点とセルをvtkPolyDataに登録．
<pre>vtkPolyData sfc
    sfc SetPoints pts
    sfc SetPolys clls
    pts Delete
    clls Delete</pre>
ファイルに保存して完了．
<pre>vtkPolyDataWriter writer
   writer SetInput sfc
   writer SetFileName sphere2.vtk
   writer Write
   writer Delete
sfc Delete</pre>