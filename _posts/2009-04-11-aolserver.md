---
id: 129
title: aolserverのインストール
date: 2009-04-11T11:38:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/04/11/aolserver%e3%81%ae%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab/'
permalink: /2009/04/11/aolserver/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/04/aolserver.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1787432787383623793
categories:
  - コンピュータ
tags:
  - aolserver
  - macports
---
MacPortsからaolserver-4.5.1をインストール．
aolserverはtclで書かれているので，tclをインストールしておく．
tclは+universalなし+threadsありでインストールする．

ローカル用のソースツリー（例えば<code>/Library/MacPorts/ports_local/www/aolserver</code>）に
aolserverのPortfileをコピー．
ドキュメントをインストールするように修正．
<pre>
variant doc description {install documentation} {
    destroot.target-append install-docs
}</pre>
インデックスを更新し，インストール．
<pre>
$ cd /Library/MacPorts/ports_local
$ portindex
$ sudo port -d install aolserver +doc</pre>
<code>/opt/local/aolserver</code>の下に<code>html</code>と<code>man</code>ができる．
<code>share</code>の下に置くべきかは分からないので，maintainerに任せる．

aolserverのデーモンは<code>nsd</code>スーパーユーザでは起動できないので，wwwで起動することにする．wwwがログを書き込めるように，所有者を変更する．ログファイルとプロセスIDが<code>log</code>に作られるので，ディレクトリを作成する．<code>servers</code>以下にサイトが作られる．サイトは複数置ける．あとで，サンプル<code>servers/server1</code>を使って<code>nsd</code>を起動するが，ここにもログが出力されるので，所有者を変更しておく．
<pre>
$ sudo mkdir /opt/local/aolserver/log
$ sudo chown /opt/local/aolserver/log www
$ sudo chown -R /opt/local/aolserver/servers/server1</pre>
Foreground (<code>-f</code>) で<code>nsd</code>を起動する．
<pre>
$ sudo bin/nsd -u www -ft base.tcl</pre>
IPアドレス:8000にアクセスすると，設定情報が表示される．