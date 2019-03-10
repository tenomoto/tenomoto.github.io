---
id: 87
title: pandocで日本語epub
date: 2010-08-03T14:18:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2010/08/03/pandoc%e3%81%a7%e6%97%a5%e6%9c%ac%e8%aa%9eepub/'
permalink: /2010/08/03/pandoc-japanese-epub/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2010/08/pandocepub_03.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/7890274341518660055
categories:
  - コンピュータ
tags:
  - epub
  - pandoc
---
pandocでepubを作る時, metadata.xmlに言語を指定できるが, content.opfに書き込まれるだけで, 個々のxhtmlには言語は指定されない. このままだとAdobe Digital Editionsでは文字化けしてしまう. 横浜工文社のbatスクリプトを参考にpandocが生成したepubを解凍, xhtmlを編集, 再びepubにまとめるスクリプトを作成した.
<pre>
#!/bin/sh
epub=$1
bname=`basename ${epub}`
base=${bname%.*}
epubo=${base}_jp.epub
TMPDIR=/tmp/${base}

if [ -d ${TMPDIR} ]; then
  rm -rf ${TMPDIR}
fi
if [ -f ${TMPDIR}/../${epubo} ]; then
  rm -f ${TMPDIR}/../${epubo}
fi
if [ -f ${epubo} ]; then
  rm -f ${epubo}
fi
mkdir ${TMPDIR}

unzip ${epub} -d ${TMPDIR}

cd ${TMPDIR}
for f in *.xhtml; do
  g=${f}j
  sed -e 's|html xmlns="http://www.w3.org/1999/xhtml"|html xmlns="http://www.w3.org/1999/xhtml" xml:lang="ja" lang="ja"|' ${f} &gt; ${g}
  mv -f ${g} ${f}
done

zip -0 ../${epubo} mimetype
zip -r ../${epubo} * -x mimetype

mv ../${epubo} ${OLDPWD}
rm -rf ${TMPDIR}
rm -f ${TMPDIR}../${epubo}</pre>