---
id: 39
title: HakyllでMathJaxを使う
date: 2013-03-26T15:18:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2013/03/26/hakyll%e3%81%a7mathjax%e3%82%92%e4%bd%bf%e3%81%86/'
permalink: /2013/03/26/hakyll-mathjax/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2013/03/hakyllmathjax.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3975545204897448153
categories:
  - コンピュータ
tags:
  - Hakyll
  - Haskell
  - MathJax
  - static site generator
---
静的サイト生成ツールHakyllの強みは，Pandocを使ってテキスト処理をしていること。PandocはMathJax出力ができるので，Hakyllを使って生成するサイトにもMathJaxが使えるはずである。<!--more-->

hakyll-initした既定のままでは，MathJaxは利用できない。Hakyllの設定ファイルは，Haskellソース。Qnikst blogの<a href="http://qnikst.github.com/posts/2013-02-04-hakyll-latex.html">ポスト</a>を参考にsite.hsを修正する。
<h3>site.hsの編集</h3>
まず，ライブラリを追加する。
<pre>import           qualified Data.Map as M
import           Text.Pandoc</pre>
Pandocにオプションを渡すために，pandocCompilerではなく，pandocCompilerWithを使う。オプションと言ってもコマンドラインオプションではなく，Pandocの<a href="http://hackage.haskell.org/package/pandoc">API</a>の引数として渡す。
<pre>    match "posts/*" $ do
        route $ setExtension "html"
        compile $ pandocCompilerWith defaultHakyllReaderOptions pandocOptions
            &gt;&gt;= saveSnapshot "content"
            &gt;&gt;= return . fmap demoteHeaders
            &gt;&gt;= loadAndApplyTemplate "templates/post.html" postCtx
            &gt;&gt;= loadAndApplyTemplate "templates/default.html" (mathCtx `mappend` postCtx)</pre>
ここでは，template/default.htmlでMathJaxを使う。このテンプレートを適用する際に，mathCtxによりタグ$mathjax$を調べる。数式を使う場合にのみ，MathJaxのJavaScriptを読むようにする。このテンプレートは，数箇所使われているのでmappendを使い適宜mathCtxを追加する。 mathCtxの定義はbloggerでうまく表示できないので上記ポスト参照。
<h3>pandocOptionsの定義</h3>
<pre>pandocOptions :: WriterOptions
pandocOptions = defaultHakyllWriterOptions{ writerHTMLMathMethod = MathJax "" }</pre>
<h3>templates/default.htmlの編集</h3>
$mathjax$が空のときに空行が入らないようにcssと同じ行にタグを付けた。
<pre>       $mathjax$</pre>
<h3>数式入り投稿の例</h3>
<pre>---
title: MathJax
mathjax: on
---
$sqrt{frac{1}{2}}$はinline math.
$$sqrt{frac{1}{2}}$$はdisplay math.</pre>