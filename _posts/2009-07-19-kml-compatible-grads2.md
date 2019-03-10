---
id: 124
title: KML対応grads2
date: 2009-07-19T16:38:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/07/19/kml%e5%af%be%e5%bf%9cgrads2/'
permalink: /2009/07/19/kml-compatible-grads2/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/07/kmlgrads2.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1436409304017354018
categories:
  - コンピュータ
tags:
  - GrADS
  - macports
---
MacPortsのgrads2を2.0.a5.oga.5にアップグレード.

このバージョンの特長は, Google Earthに結果を表示するKMLに<a href="http://www.iges.org/grads/gadoc/gradcomdsetkml.html">対応</a>したこと.

MacPortsのgrads2では+geotiffをつける.
ラスター形式のファイル出力に便利な+printimもついでにつけてインストールする例.
<pre>
sudo port -d install grads2 +geotiff +printim</pre>
netcdf4に対応するとのことで, しばらく格闘していた. configure.acなどを解読して, --enable-dyn-supplibsをつけないで静的ライブラリをリンクするようにすると, netcdf4を探してくれることをようやく理解. 現状では, hdf5-18やlibgeotiffは静的ライブラリをインストールしない. しない理由はなさそうだが. 一応コンパイルはできたが, grads-2を起動したディレクトリに変なファイルができてしまうこと, x軸を探せずにsdfopenができなかったことから, 当面netcdf4対応は見送り, 復活させたnetcdf3にリンクすることにした.

これでnetcdf4騒動は一段落.

grads2に含まれるコマンドは-2がつくので注意 (grads-2, gradsdap-2など). grads2が作るwgribはwgrib2ではないwgribだが, バイナリ名はwgrib-2. gradsのwgribと同等だと思われる. wgrib2がインストールするバイナリはwgrib2.