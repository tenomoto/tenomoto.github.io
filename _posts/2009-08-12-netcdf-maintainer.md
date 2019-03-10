---
id: 116
title: netcdfのmaintainer
date: 2009-08-12T10:01:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/08/12/netcdf%e3%81%aemaintainer/'
permalink: /2009/08/12/netcdf-maintainer/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/08/netcdfmaintainer.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3812016962737941386
categories:
  - コンピュータ
tags:
  - macports
  - NetCDF
---
MacPortsのnetcdfのmaintainerをすることにした. netcdfに依存するパッケージの大半は自分が管理しているので, netcdfを自由にできた方が都合が良い.
<div></div>
<div>--enable-netcdf-4はvariantにまわして, netcdf3にリンクしていたgrads, grads2, gmtもnetcdfにリンクしてコンパイルできるようにした. netcdf 3は削除.</div>
<div><span style="font-family: arial, sans-serif; font-size: 100%;"><span style="border-collapse: collapse; font-size: 13px;"><span style="font-family: Georgia, fantasy; font-size: 130%;"><span style="border-collapse: separate; font-size: 16px;"> </span></span></span></span></div>
<div><span style="font-family: Georgia, -webkit-fantasy;">nco, cdo, wgrib2は, netcdf4にvariantで対応.</span></div>