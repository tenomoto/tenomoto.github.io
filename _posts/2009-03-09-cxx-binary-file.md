---
id: 137
title: C++でバイナリファイルを読む
date: 2009-03-09T19:54:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/03/09/c%e3%81%a7%e3%83%90%e3%82%a4%e3%83%8a%e3%83%aa%e3%83%95%e3%82%a1%e3%82%a4%e3%83%ab%e3%82%92%e8%aa%ad%e3%82%80/'
permalink: /2009/03/09/cxx-binary-file/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/03/c_09.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7458791302724430621
categories:
  - コンピュータ
tags:
  - CXX
---
<pre>#include &lt;fstream&gt;

std::ifstream f;

f.open(filename, std::ios::in | std::ios::binary);
f.seekg(pos);
f.read((char*)data, size);
f.close();</pre>
openするときの二つ目の引数がポイント．