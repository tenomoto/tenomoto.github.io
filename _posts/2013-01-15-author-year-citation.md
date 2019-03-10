---
id: 42
title: 著者 出版年 形式での引用
date: 2013-01-15T11:52:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2013/01/15/%e8%91%97%e8%80%85-%e5%87%ba%e7%89%88%e5%b9%b4-%e5%bd%a2%e5%bc%8f%e3%81%a7%e3%81%ae%e5%bc%95%e7%94%a8/'
permalink: /2013/01/15/author-year-citation/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2013/01/blog-post.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4892340758610365325
categories:
  - コンピュータ
tags:
  - TeX
---
TeXのデフォルトは，文献に振った番号で引用する。気象等では，著者 (年)の形式で引用するので，natbibパッケージを使う。

<!--more-->
<pre>usepackage{natbib}
bibliographystyle{ametsoc}
setcitestyle{aysep={}}</pre>
<div>bibliographystyleはplainnatが基本だが，上記の例では米国気象学会の<a href="http://www.ametsoc.org/pubs/journals/manuscripttemplates.html">テンプレート</a>に含まれているametsoc.bst利用している。setcitestyleで，著者と出版年との間の記号 aysep の「,」を削除している。</div>
ametsoc.bstは号を()の中に入れて出力する。これを取り除くには，FUNCTION {format.vol.num.pages}の
<pre>  number "number" bibinfo.check duplicate$ empty$ 'skip$
    {    
      swap$ duplicate$ empty$
        { "there's a number but no volume in " cite$ * warning$ }
        'skip$
      if$  
      swap$
      ""  * "" * 
    }    
  if$ *</pre>
を削除する。