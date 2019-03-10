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
Macの共有ライブラリには，インストール先の情報が記録される．インストール先は，-install_nameの指定があればそのディレクトリ，なければ-oで指定したものが使われる．ライブラリのinstall nameは，これをリンクしたライブラリやバイナリに転写されていく．<br /><br />-install_nameの後はスペース．=を入れると正しく動作しないので注意．<br /><br />オブジェクトファイルに関する情報は，otoolで表示することができる．<br />ライブラリの名前とバージョン，リンクしているオブジェクトやライブラリを表示するには，<br /><pre>otool -L ライブラリまたはバイナリ</pre><br />ライブラリのinstall nameを表示するには，<br /><pre>otool -D ライブラリ</pre><br />を使う．<br /><br />共有ライブラリのinstall nameの変更は，install_name_toolを使う．<br /><pre>install_name_tool -id 新しいパス</pre><br />でできる．ライブラリやバイナリに書き込まれた他のライブラリのinstall nameを変更するには，<br /><pre>install_name_tool -change 古いパス 新しいパス</pre><br />とする．<br /><br />多くのフリーウェアでは，libtoolがこのあたりの面倒を見てくれるが，シェルスクリプトやGNU Makeを駆使して機種依存の問題を解消しようとしているものもある．<br /><br />vaporは，configureの変わりにoptions.mk, site.mkを手動で編集したり，機種依存のインクルードファイル（例: Darwin.mk）を用意している．ライブラリには，生成したディレクトリのパスがinstall_nameとして記録されているため，うまく動作しない．DYLD_LIBRARY_PATHを設定してライブラリを見つけようとしている．既定の-two_levelnamespaceだとコマンドラインと共有ライブラリに記録されたパスしか検索しないので，ライブラリは見つからない．<br /><br />make/config/Darwin.mkのSHARED_LDFLAGSに-install_nameを指定して対処．