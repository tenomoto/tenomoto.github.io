---
id: 43
title: PDFにページ番号を振る
date: 2013-01-09T15:41:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2013/01/09/pdf%e3%81%ab%e3%83%9a%e3%83%bc%e3%82%b8%e7%95%aa%e5%8f%b7%e3%82%92%e6%8c%af%e3%82%8b/'
permalink: /2013/01/09/pdf-page-numbering/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2013/01/pdf.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/4960660591833837182
categories:
  - コンピュータ
tags:
  - macports
  - PDF
  - TeX
---
講演者に送っていただいた，PDF形式の講演要旨にページ番号を付ける。Acrobatでもできるが，講演は50件以上あるので，ひとひとつファイルを開いて作業するのは手間がかかる上，ミスをしやすい。そこで，コマンドラインで作業することにする。<!--more-->

まず，ページ数を勘定する必要がある。<a href="http://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/">pdfk</a>を使うとPDFの情報を表示できる。
<pre>pdftk foo.pdf dump_data output - | grep NumberOfPages | awk '{print $2}</pre>
pdftkは，バイナリも配布されているが，MacPortsでインストールすることもできる。一時期gcjの問題でコンパイルできないことがあったが，Leopardではgcc42，Snow Leopardでは gcc45，LionとMountain Lionではgcc47が既定で選択されてコンパイルに使用される。

ページ番号はLaTeXに振ってもらう。印刷範囲を無視して複数ページのPDFを取り込むには，pdfpagesパッケージを用いる。

以下にテンプレートを示す。Nは開始するページ番号，PDFはPDFのファイル名が入る。
<pre>%!TEX TS-program = pdflatex
documentclass[11pt]{article}
usepackage{pdfpages}

begin{document}

setcounter{page}{N}
setlength{footskip}{3cm}
includepdf[pages=-,pagecommand={thispagestyle{plain}}]{PDF}</pre>
<pre></pre>
includepdfのオプションpages=-は全てのページを取り込むことを示す。既定は最初のページのみ。pagecommand={thispagestyle{plain}}でページを振ることを示す。ページ番号が本文に重なってしまったので，footskipで調整している。私の試した範囲では，geometryパッケージを使うとページ番号が表示されなかった。

pdfpagesは，MacPortsのtexlive-latex-recommendedに含まれている。