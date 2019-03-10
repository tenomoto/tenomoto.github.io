---
id: 636
title: C++でのファイルの読み込み
date: 2016-04-27T14:48:05+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/?p=636
permalink: /2016/04/27/cxx-read-text-binary/
categories:
  - コンピュータ
tags:
  - cplusplus
---
ファイルの入出力はプログラミング言語の本の比較的後ろの方に出てくるが，データを扱う場合データが読めないと始まらない。<!--more-->

Armadilloやmlpackを使ってみたいので，C++でテキストファイルやバイナリファイルを読んでみる。C++のストリームはバイトの列なのでいろいろな複雑なものを読み書きするのに使えるが，読みたいデータは複雑なものではなく同じ型のものが並んでいるだけだ。

<h4>テキストファイル</h4>
入力ストリーム（<code>if stream</code>）を開いて<code>>></code>で読めるだけ読む。C++らしいところは，型をパラメタ化しているところ，動的配列std::vectorを使っているところ。

https://gist.github.com/tenomoto/75a8fabb09f010b30d65d4e9a2bcaa8f

<h4>バイナリファイル</h4>
直接アクセスの場合。<code>ifs</code>をバイナリモード（<code>std::ios::binary</code>）で開いた入力ストリームとする。数値予報モデルの名前ではない。<code>ifs.read()</code>を使って1文字（<code>char</code>）ずつデータを読む。エンディアンをひっくり返すには文字配列の後ろから読めば良い。

https://gist.github.com/tenomoto/2f4d422530397bb736525c9ce0fa5c0f
