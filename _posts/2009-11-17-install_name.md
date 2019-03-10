---
id: 103
title: install_name
date: 2009-11-17T16:17:00+09:00
author: takeshi
layout: post
guid: https://www.enomosphere.net/2009/11/17/install_name/
permalink: /2009/11/17/install_name/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/11/installname.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/3090986577811375027
categories:
  - コンピュータ
tags:
  - Mac
  - macports
  - vapor
---
Macの共有ライブラリには，インストール先の情報が記録される．インストール先は，-install_nameの指定があればそのディレクトリ，なければ-oで指定したものが使われる．ライブラリのinstall nameは，これをリンクしたライブラリやバイナリに転写されていく．

-install_nameの後はスペース．=を入れると正しく動作しないので注意．

オブジェクトファイルに関する情報は，otoolで表示することができる．
ライブラリの名前とバージョン，リンクしているオブジェクトやライブラリを表示するには，

```bash
$ otool -L ライブラリまたはバイナリ
```

ライブラリのinstall nameを表示するには，

```bash
$ otool -D ライブラリ
```

を使う．

共有ライブラリのinstall nameの変更は，install_name_toolを使う．

```bash
$ install_name_tool -id 新しいパス
```

でできる．ライブラリやバイナリに書き込まれた他のライブラリのinstall nameを変更するには，


```bash
$ install_name_tool -change 古いパス 新しいパス
```
とする．

多くのフリーウェアでは，`libtool`がこのあたりの面倒を見てくれるが，シェルスクリプトやGNU Makeを駆使して機種依存の問題を解消しようとしているものもある．

vaporは，`configure`の変わりに`options.mk`, `site.mk`を手動で編集したり，機種依存のインクルードファイル（例: `Darwin.mk`）を用意している．ライブラリには，生成したディレクトリのパスが`install_name`として記録されているため，うまく動作しない．`DYLD_LIBRARY_PATH`を設定してライブラリを見つけようとしている．既定の`-two_levelnamespace`だとコマンドラインと共有ライブラリに記録されたパスしか検索しないので，ライブラリは見つからない．

`make/config/Darwin.mk`の`SHARED_LDFLAGS`に`-install_name`を指定して対処．