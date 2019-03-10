---
id: 955
title: SQLiteを5分以内で
date: 2019-01-20T14:24:50+09:00
author: takeshi
layout: page
guid: https://www.enomosphere.net/?page_id=955
classic-editor-remember:
  - classic-editor
---
<!-- wp:paragraph -->
<p><a href="https://www.sqlite.org/quickstart.html">SQLite In 5 Minutes Or Less</a>の拙訳</p>
<p>SQLiteを試してみるには，以下のことをやってみましょう。たくさんのドキュメントを読む必要も，面倒な設定も不要です。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>コードをダウンロードする</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>あなたのパソコンで動くコンパイル済バイナリのコピーを入手するか，ソースのコピーを入手して自分でコンパイルしてください。<a href="https://www.sqlite.org/download.html">ダウンロード</a>ページには詳しい情報が書かれています。</li>
</ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>新しいデータベースを作成する</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>シェルまたはDOSプロンプトで<strong>sqlite3 test.db</strong>と入力してください。test.dbという名前の新しいデータベースが作成されます。（これとは違うお好みの名前でも構いません。）</li>
<li>SQLコマンドをプロンプトに打てば，新しいデータベースを作成し，データを入力することができます。</li>
<li>追加のドキュメントはこちらにあります。</li>
</ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>SQLiteを使うプログラムを書く</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>以下は簡単な<a href="http://www.tcl-lang.org/">Tclプログラム</a>で，SQLiteのTclインターフェースの使い方を示しています。プログラムは2番目の引数として与えられたSQL文を最初の引数で定義されたデータベースに対して実行します。注目すべきコマンドは，7行目の<strong>sqlite3</strong>コマンドで，SQLiteデータベースを開き，そのデータベースにアクセスする新しいオブジェクト<strong>db</strong>を作成します。 8行目の <strong>db</strong>オブジェクトの<a href="https://www.sqlite.org/tclsqlite.html#eval">evalメソッド</a>を使い，データベースに対してSQLコマンドを実行し，スクリプトの最後の行でデータベースに対する接続を解除しています。</li>
</ul>
<!-- /wp:list -->

<!-- wp:html -->
<blockquote>
<pre>01  #!/usr/bin/tclsh
02  if {$argc!=2} {
03    puts stderr "Usage: %s DATABASE SQL-STATEMENT"
04    exit 1
05  }
06  package require sqlite3
07  <strong>sqlite3</strong> db [lindex $argv 0]
08  <strong>db</strong> eval [lindex $argv 1] x {
09    foreach v $x(*) {
10      puts "$v = $x($v)"
11    }
12    puts ""
13  }
14  <strong>db</strong> close
</pre>
</blockquote>
<!-- /wp:html -->

<!-- wp:list -->
<ul>
<li>次は簡単なCのプログラムを使ってSQLiteの<a href="https://www.sqlite.org/c3ref/intro.html">C/C++インターフェースの使い方</a>を示します。データベースの名前は最初の引数，2番目の引数はデータベースに対して実行する一つ以上のSQL文です。ここで注目すべき関数呼び出しは，22行目のデータベースを開く<a href="https://www.sqlite.org/c3ref/open.html">sqlite3_open()</a>，28行目のデータベースに対してSQL文を実行するsqlite3_exec(), 33行目のデータを閉じる<a href="https://www.sqlite.org/c3ref/close.html">sqlite3_close()</a>です。</li>
</ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><a href="https://www.sqlite.org/cintro.html">SQLite C/C++インターフェース入門</a>には，初心者向けの概要とたくさんのSQLiteインターフェース関数の道案内が掲載されていますので，併せてご覧してください。</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<blockquote>
<pre>01  #include &lt;stdio.h&gt;
02  #include &lt;sqlite3.h&gt;
03  
04  static int callback(void *NotUsed, int argc, char **argv, char **azColName){
05    int i;
06    for(i=0; i&lt;argc; i++){
07      printf("%s = %s\n", azColName[i], argv[i] ? argv[i] : "NULL");
08    }
09    printf("\n");
10    return 0;
11  }
12  
13  int main(int argc, char **argv){
14    <b>sqlite3</b> *db;
15    char *zErrMsg = 0;
16    int rc;
17  
18    if( argc!=3 ){
19      fprintf(stderr, "Usage: %s DATABASE SQL-STATEMENT\n", argv[0]);
20      return(1);
21    }
22    rc = <b>sqlite3_open</b>(argv[1], &amp;db);
23    if( rc ){
24      fprintf(stderr, "Can't open database: %s\n", sqlite3_errmsg(db));
25      <b>sqlite3_close</b>(db);
26      return(1);
27    }
28    rc = <b>sqlite3_exec</b>(db, argv[2], callback, 0, &amp;zErrMsg);
29    if( rc!=SQLITE_OK ){
30      fprintf(stderr, "SQL error: %s\n", zErrMsg);
31      <b>sqlite3_free</b>(zErrMsg);
32    }
33    <b>sqlite3_close</b>(db);
34    return 0;
35  }
</pre>
</blockquote>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>上に示したプログラムのコンパイルの仕方やヒントについては<a href="https://www.sqlite.org/howtocompile.html">SQLiteのコンパイル方法</a>を参照してください。</p>
<!-- /wp:paragraph -->