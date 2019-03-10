---
id: 118
title: Exif情報の消去
date: 2009-08-02T15:59:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/08/02/exif%e6%83%85%e5%a0%b1%e3%81%ae%e6%b6%88%e5%8e%bb/'
permalink: /2009/08/02/erase-exif/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/08/exif.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6987259452351095047
categories:
  - コンピュータ
tags:
  - ImageMagick
---
Exif情報も一種の個人情報. ImageMagickでExifなどを消すには,
<div></div>
<div>-strip strip image of all profiles and comments</div>
<div></div>
<div>オプションを使う.</div>
<div></div>
<div>convert -strip foo.jpg foo_strip.jpg</div>
<div></div>