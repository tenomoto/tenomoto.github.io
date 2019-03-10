---
id: 126
title: netcdf 4騒動
date: 2009-07-18T22:24:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/07/18/netcdf-4%e9%a8%92%e5%8b%95/'
permalink: /2009/07/18/netcdf-4-confusion/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/07/netcdf-4.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/187059636771839394
categories:
  - コンピュータ
tags:
  - macports
  - NetCDF
---
有志でパッケージ管理をしていると, maintainerの中には連絡が取れなくなる人もいる. netcdfはいつの間にかnomaintainerとなっていた. そのまま放置されていただけならまだましだったのだが, どなたたかがnetcdf 4にアップグレードしてくれていた. netcdfに依存するライブラリが軒並みコンパイルできなくなって, 大迷惑だった. とりあえずnetcdf4の機能を分離してdefault variantsに指定, -netcdf4でオフにできるようにした.

netcdf 4は上位互換であるが, HDF5と統合されたので，リンクのときにHDF5のライブラリも指定する必要がある. 必要なライブラリは, pkg-configを使って,
<pre>
$ nc-config --libs</pre>
などととして取得する.

cdo, ncoはnetcdf4に対応していたので, 依存するライブラリの指定やconfigure.argsの変更で済んだ. ただし, ncoはHAVE_NETCDF4_Hがconfig.hに書き込まれないので，陽に指定する必要があった. wgrib2, gnudatalanguage, vis5d+は-lnetcdf以外のリンクするライブラリを指定する必要があった. gmtとgradsは, netcdf3を復活させて, そちらにリンクするようにした. netcdf3は${prefix}/local/lib/netcdf3に「隠して」ある.

grads2はnetcdf4に対応しているはずだが, configureがnetcdf4を検知する部分をスキップしてしまう. Google EarthのKMLファイルが作れるので, 早く提供したいのだがまだ作業が必要なようだ.

netcdfでないけど, ついでに. gnudatalanguageは, aclocal.m4をconfigureの前に再作成して, use_autoconf yesとして, configureを作り直す必要があった. HDF5の古いAPIを使うために, -DH5_USE_16_APIをconfigure.cxxflagsに追加.