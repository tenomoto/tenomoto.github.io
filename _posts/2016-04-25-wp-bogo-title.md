---
id: 631
title: WordPress+bogoでサイトのタイトルとキャッチフレーズを多言語化
date: 2016-04-25T11:26:24+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=631
permalink: /2016/04/25/wp-bogo-title/
categories:
  - コンピュータ
tags:
  - PHP
  - WordPress
---
WordPressのプラグインbogoは，ややこしくせずにサイトを多言語化できる。サイトのタイトルとキャッチフレーズを多言語にするには，テーマを編集する必要がある。
<!--more-->

<h4>子テーマの作成</h4>
編集したテーマをアップグレードすると，改変部分は消えてしまうので，<a href="https://wpdocs.osdn.jp/子テーマ">子テーマ</a>を作成する。子テーマを作るには，<code>wp-content/themes</code>にディレクトリを作り，テーマに必須の<code>style.css</code>を作成する。スタイルシートはスタイルシートヘッダで開始する。<code>Template</code>に親テーマの<code>Text Domain</code>を書く。子テーマで定義されたスタイルや関数は親テーマのものを上書きして用いられる。子テーマを作るだけなら，<code>Text Domain</code>は必須ではないが，関数から参照するので<code>Text Domain</code>を記述しておく。親テーマに<code>-child</code>をつけるのが慣例のようである。

https://gist.github.com/tenomoto/00a51401cfe1a96a612916264a863dbc#file-style-css

<h4>コードの記述</h4>
<code>function.php</code>に次のようなコードを記述する。タイトルとキャッチフレーズを表示する処理にフックするフィルタを定義して，翻訳を処理をするようにしている。ここで定義した<code>tr_option_blogname</code>と<code>tr_option_blogdescription</code>の二つ目の引数に<code>style.css</code>に書いた子テーマの<code>Text Domain</code>を記述する。さらに翻訳をするためのアクションを追加する。<code>my_child_theme_setup</code>の最初の引数は子テーマの<code>Text Domain</code>で二つ目の引数は翻訳ファイルを置いたディレクトリ。ここではテーマの中に<code>languages</code>を作り，その中に入れている。

https://gist.github.com/tenomoto/00a51401cfe1a96a612916264a863dbc#file-function-php

<h4>翻訳ファイルの準備</h4>
親テーマの翻訳ファイルをコピーし，子テーマの<code>languages</code>に追加する。<code>ja.po</code>に以下を追加する。

https://gist.github.com/tenomoto/00a51401cfe1a96a612916264a863dbc#file-ja-po

PoeditをMacPortsでインストール。
<pre>$ sudo port -d install poedit
</pre>
<code>ja.po</code>をPoeditで開き保存し<code>ja.mo</code>を作る。言語が設定されていないというエラーが出たら，「カタログ&gt; 設定」メニューを開き，「翻訳の設定」タブの言語にJapaneseと入力してOKをクリック。<code>ja.po</code>を<code>languages</code>に設置する。
<h4>参考</h4>
<ul>
	<li><a href="http://designhack.slashlab.net/how-to-make-multilingual-wordpress-site-title-and-tagline-with-bogo-plugin/">WordPress のサイト名とキャッチフレーズを多言語化する方法 with Bogo プラグイ</a></li>
	<li><a href="http://hirsky.com/363.html">WordPressの子テーマで翻訳多言語対応する方法</a></li>
</ul>