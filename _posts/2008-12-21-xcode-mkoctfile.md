---
id: 157
title: Xcodeでmkoctfile
date: 2008-12-21T15:57:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2008/12/21/xcode%e3%81%a7mkoctfile/'
permalink: /2008/12/21/xcode-mkoctfile/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2008/12/xcodemkoctfile.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/6534641334010680582
image: /wp-content/uploads/2008/12/project-672x372.png
categories:
  - コンピュータ
tags:
  - C
  - Mac
  - Octave
---
XcodeのビルドシステムはGNU Makeではないが，少しカスタマイズすれば，任意のコンパイラやスクリプトを実行することが可能である．ここでは，Octaveのライブラリにリンクするスタンドアロンのバイナリを作成してみる．<a href="https://www.enomosphere.net/wp-content/uploads/2008/12/project.png"><img id="BLOGGER_PHOTO_ID_5282136207879711842" style="margin: 0pt 0pt 10px 10px; float: right; cursor: pointer; width: 200px; height: 154px;" src="https://www.enomosphere.net/wp-content/uploads/2008/12/project-300x230.png" alt="" border="0" /></a>

まず，Xcodeを起動しプロジェクトを作成する．プロジェクトの種類が並んでいる左側からCommand Line Utilityを選ぶ．右側からStandard Toolを選ぶ．プロジェクト名はhellooとして適当な場所に保存する．プロジェクト名と同じ名前のディレクトリが自動的に作成されて，プロジェクトファイルhelloo.xcodeprojやサンプルソースがこのディレクトリに作成される．<a href="https://www.enomosphere.net/wp-content/uploads/2008/12/source.png"><img id="BLOGGER_PHOTO_ID_5282140515053178002" style="margin: 0pt 10px 10px 0pt; float: left; cursor: pointer; width: 200px; height: 136px;" src="https://www.enomosphere.net/wp-content/uploads/2008/12/source-300x203.png" alt="" border="0" /></a>

main.cやhelloo.1は不要なので，プロジェクトのウィンドウで選択して削除する．ファイルメニューから新規ファイルを選択してhelloo.ccというファイルを作成する．テンプレートはその他から空のファイルを選ぶ．このファイルにOctaveのマニュアルにある<a href="http://www.gnu.org/software/octave/doc/interpreter/Standalone-Programs.html#Standalone-Programs">例</a>をコピーして保存．この例にはバグがあるのだが，ここではそのままにしておく．


<a href="https://www.enomosphere.net/wp-content/uploads/2008/12/target.png"><img id="BLOGGER_PHOTO_ID_5282139296343158434" style="margin: 0pt 0pt 10px 10px; float: right; cursor: pointer; width: 168px; height: 200px;" src="https://www.enomosphere.net/wp-content/uploads/2008/12/target-252x300.png" alt="" border="0" /></a>
プロジェクトウィンドウ左側のターゲット，さらにhellooも開く．3段階のフェーズのうち，ソースのコンパイル以外は不要なので削除する．次に，ソースのコンパイルをカスタマイズしてmkoctfileを呼ぶようにする．ターゲット&gt;hellooを選択した状態でボタンバーの情報をクリック．Command+iでもよい．ルールタブをクリックして表示したら，左下の+ボタンをクリックしてルールを追加する．プロセスは同名のファイルとして，*.ccと入力する．使用はカスタムスクリプトとし
<pre>/opt/local/bin/mkoctfile --link-stand-alone ${INPUT_FILE_DIR}/${INPUT_FILE_NAME} -o ${TARGET_BUILD_DIR}/${INPUT_FILE_BASE}</pre>
と入力する．出力ファイルを追加し
<pre>${TARGET_BUILD_DIR}/${INPUT_FILE_BASE}</pre>
と入力する．ここで用いた環境変数は，右下のボタン?をクリックして表示されるマニュアルに説明されている．

ビルドをクリックしてビルドしてみる．二重forループの中に
<pre>a_matrix(row,column)</pre>
となっていればエラー箇所として指摘されているはずである．row, columnは定義されておらず，おそらくi, jの誤りだろう．ここを修正すればコンパイルが通るはずである．

ビルドして実行ボタンをクリックしても，コマンドラインツールなので，何も表示されない．結果はツールからコンソールを選べば表示できる．プロジェクトウィンドウのProductの下に表示されるhellooをダブルクリックするとターミナルが開いてバイナリが実行される．

mkoctfileは，シェルスクリプトで，コンパイルにはg++が呼ばれている．Xcodeでは，g++のエラーメッセージを解釈して，エディタに該当箇所を表示できるので，効率的な開発役立ちそうである．MPIやOpenGLのプログラムは，同様な方法でmpiccやglccを呼べばよさそうである．シェルスクリプトが面倒を見てくれるので，ヘッダやライブラリをプロジェクトに追加する手間が不要だ．C, C++のラッパ以外でも同様の方法で良い．ただし，g95, gfortranだと，エラーメッセージは正しく解釈されない．エラーメッセージは，ソースの上に表示される．