---
id: 966
title: SQLiteのコマンドラインシェル
date: 2019-01-20T14:25:09+09:00
author: takeshi
layout: page
guid: https://www.enomosphere.net/?page_id=966
classic-editor-remember:
  - block-editor
---
<!-- wp:paragraph -->
<a href="https://www.sqlite.org/cli.html">Command-Line Shell (sqlite3.exe)</a>の拙訳
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>関連リンク</h2>

<!-- /wp:heading -->

<!-- wp:list -->

<ul><li><a href="https://amzn.to/2CBcpUf">シェルスクリプト+データベース活用テクニック</a></li><li><a href="https://qiita.com/tenomoto/items/6ffc078d2cdcd4741ac1">テキスト処理とSQLの比較</a></li></ul>

<!-- /wp:list -->

<!-- wp:heading -->

<h2>1. はじめよう</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
SQLiteプロジェクトが提供している<strong>sqlite3</strong>（Windowsでは<strong>sqlite3.exe</strong>）という名前の簡単なコマンドラインプログラムを使えば，ユーザがSQLデータベースに対してSQL文を手入力し実行できます。このドキュメントでは，<strong>sqlite3</strong>の使い方を簡単に紹介します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>sqlite3</strong>を起動するには，コマンドプロンプトでsqlite3とタイプしてください。続けてSQLiteデータベースを格納するファイル名を指定することもできます。名前を指定したファイルがない場合は，与えた名前の新しいデータベースファイルが自動的に生成されます。データベースファイルがコマンドラインに指定されていない場合は，一時的なデータベースが作成され，sqliteプログラムの終了時に削除されます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
起動時に<strong>sqlite3</strong>プログラムは短いバナーメッセージを表示し，SQLを入力するためのプロンプトを表示します。SQL文（セミコロンで区切る）をタイプし，Enterを押せばSQLが実行されます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
例えば，ex1という名前の新しいSQLiteデータベースにtbl1というテーブルを一つ作成するには，次のようにすればよいでしょう。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>$ <b>sqlite3 ex1</b>
SQLite version 3.8.5 2014-05-29 12:36:14
Enter ".help" for usage hints.
sqlite&gt; <b>create table tbl1(one varchar(10), two smallint);</b>
sqlite&gt; <b>insert into tbl1 values('hello!',10);</b>
sqlite&gt; <b>insert into tbl1 values('goodbye', 20);</b>
sqlite&gt; <b>select * from tbl1;</b>
hello!|10
goodbye|20
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
sqlite3プログラムを終了するにはシステムのEnd-Of-File文字（通常はControl-D）をタイプします。中断文字（通常はControl-C）は長い間走っているSQL文を止めるときに使います。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
SQLコマンド毎にセミコロンをタイプするのを忘れないように！sqlite3プログラムは，セミコロンを見つけるとSQLコマンドが終わりだと知ることができます。セミコロンを省略すると，sqlite3は継続プロンプトを表示し，これまでのSQLコマンドに追加するテキストが入力されるのを待ちます。この機能を使うと， 複数行に渡るSQLコマンドを入力することができます。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>CREATE TABLE tbl2 (</b>
   ...&gt; <b>  f1 varchar(30) primary key,</b>
   ...&gt; <b>  f2 text,</b>
   ...&gt; <b>  f3 real</b>
   ...&gt; <b>);</b>
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:heading -->

<h2>2. Windowsでのダブルクリック起動</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
Windowsユーザは，sqlite3.exeのアイコンをダブルクリックできます。すると，コマンドラインシェルによってSQLiteが動作しているターミナルを立ち上がります。ただし，ダブルクリックだとsqlite3.exeは引数なしで起動するので，データベースは指定されていません。SQLiteは一時的なデータベースを使い，セッションが終わるとデータベースは削除されてしまいます。永続的なディスク上のファイルをデータをとして使うには，ターミナルウィンドウが起動したらすぐに.openコマンドを入力してください。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>SQLite version 3.8.5 2014-05-29 12:36:14
Enter ".help" for usage hints.
Connected to a transient in-memory database.
Use ".open FILENAME" to reopen on a persistent database.
sqlite&gt; <b>.open ex1.db</b>
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
上の例はex1.dbという名前のデータベースファイルが開かれて使用されます。ex1.dbファイルは既存のものがなければ作成されます。絶対パスを使って，思ったディレクトリにファイルが確実に作成したい場合があるかもしれません。その際は，前方スラッシュをディレクトリの区切り文字として使ってください。つまり，c:/work/ex1.dbでc:\work\ex1.dbではありません。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
もしくは，既定の一時ストレージをを使った新しいデータベースを作成し，データベースをディスクに保存するのに.saveコマンドを使うこともできます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>SQLite version 3.16.0 2016-12-29 19:48:46
Enter ".help" for usage hints.
Connected to a transient in-memory database.
Use ".open FILENAME" to reopen on a persistent database.
sqlite&gt; <i>... many SQL commands omitted ...</i>
sqlite&gt; <b>.save ex1.db</b>
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:heading -->

<h2>sqlite3に対する特別コマンド（ドットコマンド）</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
通常sqlite3は入力された行を読み，それを実行するためにSQLiteライブラリに渡しているだけです。しかし入力された行がドット（.）で始まるときは，コマンドを渡さずsqlite3プログラム自体により解釈されます。これらの「ドットコマンド」は，クエリの出力フォーマットを変えたり，前もってパッケージされた文を実行したりするために用いられます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
利用可能なドットコマンド一覧を表示するには，.helpを引数なしで入力してください。.help TOPICと入力してTOPICについての詳しい情報を表示することもできます。ドットコマンドの一覧は次の通りです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.help</b>
.archive ...             SQLアーカイブを管理
.auth ON|OFF             認証コールバックを表示
.backup ?DB? FILE        DB（デフォルトmain）をFILEにバックアップ
.bail on|off             エラー発生後に停止するか。デフォルトはOFF
.binary on|off           バイナリ出力のオンオフ切り替え。デフォルトはOFF
.cd DIRECTORY            作業ディレクトリをDIRECTORYに変更
.changes on|off          SQLにより変更された行を表示
.check GLOB              .testcaseからの出力が一致しない場合はエラー
.clone NEWDB             既存データベースからNEWDBにクローン
.databases               アタッチされたデータベースの名前とファイルを表示
.dbconfig ?op? ?val?     sqlite3_db_config()オプションを表示または変更
.dbinfo ?DB?             データベースに関する情報を表示
.dump ?TABLE? ...        データベースの全ての内容をSQLで表示
.echo on|off             コマンドエコーのオンオフ切り替え
.eqp on|off|full         自動EXPLAIN QUERY PLANを有効または無効に切り替え
.excel                   次のコマンドの出力をスプレッドシートで表示
.exit ?CODE?             リターンコードCODEでこのプログラムを終了
.expert                  実験的機能。指定したクエリに適したインデックスを生成
.fullschema ?--indent?   スキーマとsqlite_statテーブルの中身を表示
.headers on|off          ヘッダ表示のオンオフ切り替え
.help ?-all? ?PATTERN?   PATTERNのヘルプを表示
.import FILE TABLE       FILEからTABLEにデータを読み込む
.imposter INDEX TABLE    インデックスINDEXの偽名テーブルTABLEを生成
.indexes ?TABLE?         インデックス名を表示
.iotrace FILE            FILEへのI/O診断ログ記録の有効化
.limit ?LIMIT? ?VAL?     SQLITE_LIMITの表示または値の変更
.lint OPTIONS            潜在的なスキーマの問題を調査
.load FILE ?ENTRY?       エクステンションライブラリのロード
.log FILE|off            ログ記録のオンオフ切り替え。FILEはstderr/stdoutも可
.mode MODE ?TABLE?       出力モードの設定
.nullvalue STRING        NULL値の代わりにSTRINGを使用
.once (-e|-x|FILE)       次のSQLコマンドに限りFILEに保存
.open ?OPTIONS? ?FILE?   既存データベースを閉じ，FILEを開き直す
.output ?FILE?           出力をFILEまたはstdout（FILE省略時）に送信
.print STRING...         リテラルSTRINGを表示
.prompt MAIN CONTINUE    標準プロンプトの置き換え
.quit                    このプログラムを終了
.read FILE               FILEから入力を読み込む
.restore ?DB? FILE       FILEからDBの内容（デフォルトmain) を復元
.save FILE               メモリ内データベースをFILEに書き出す
.scanstats on|off        sqlite3_stmt_scanstatus()メトリックのオンオフ切り替え
.schema ?PATTERN?        PATTERNにマッチするCREATE文を表示
.selftest ?OPTIONS?      SELFTESTテーブルに定義されたテストを実行
.separator COL ?ROW?     列と行の区切り文字を変更
.session ?NAME? CMD ...  セッションの生成または制御
.sha3sum ...             データベースの内容のSHA3ハッシュの計算
.shell CMD ARGS...       システムシェルでCMD ARGS...を実行
.show                    様々な設定についての現在の値を表示
.stats ?on|off?          統計を表示または統計のオンオフ切り替え
.system CMD ARGS...      システムシェルでCMD ARGS...を実行
.tables ?TABLE?          LIKEパターンTABLEでマッチするテーブル名を表示
.testcase NAME           'testcase-out.txt'に出力をリダイレクト開始
.timeout MS              MSミリ秒の間ロックされたテーブルを開いてみる
.timer on|off            SQLタイマーのオンオフ切り替え
.trace FILE|off          各SQL文を実行するたびに出力
.vfsinfo ?AUX?          トップレベルのVFSについての情報を表示
.vfslist                 利用可能なVFSを全て表示
.vfsname ?AUX?           VFSスタックの名前を表示
.width NUM1 NUM2 ...     columnモードの列幅を設定
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:heading -->

<h2>4. 「ドットコマンド」のルール</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
通常のSQL文は自由形式であり，複数行に渡って書くことができ，空白文字を含むことが可能で，どこにでもコメントが書けます。ドットコマンドには，より多くの制約があります。
<!-- /wp:paragraph -->

<!-- wp:list -->

<ul><li>ドットコマンドは，左端から.で始まり空白文字を前につけることはできない。</li><li>ドットコマンドは，全体を単一の行に書かなければならない。</li><li>ドットコマンドは，通常のSQL文の途中に書いてはならない。つまり，ドットコマンドは継続プロンプトには入力できない。</li><li>ドットコマンドはコメントを認識しない。</li><li>&nbsp;</li></ul>

<!-- /wp:list -->

<!-- wp:paragraph -->
ドットコマンドは， SQLite3自体ではなく，sqlite3.exeコマンドラインプログラムにより解釈されます。したがって，どのドットコマンドも<a href="https://www.sqlite.org/c3ref/prepare.html">sqlite3_prepare()</a>や<a href="https://www.sqlite.org/c3ref/exec.html">sqlite3_exec()</a>のようなSQLiteインターフェースの引数として動作しません。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>5. 出力形式の変更</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
sqlite3プログラムはクエリの結果を9つの異なる形式 csv, column, html, insert, line, list, quote, tabs, tclで表示できます。.modeドットコマンドを使って出力形式の切り替えが可能です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
既定の出力形式はlistです。listモードでは，クエリ結果の各行は，出力の1行に書かれ，その行に含まれる各列は特定の区切り文字で区切られます。既定の区切り文字はパイプ記号（|）です。listモードが適しているのは，出力を （AWKのような） 別のプログラムに渡して追加の処理をする場合です。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode list</b>
sqlite&gt; <b>select * from tbl1;</b>
hello|10
goodbye|20
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.separatorドットコマンドを使うと区切り文字を変更できます。例えば，区切り文字をコンマとスペースにするには，次のようにします。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.separator ", "</b>
sqlite&gt; <b>select * from tbl1;</b>
hello, 10
goodbye, 20
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
次の.modeコマンドは.separatorを既定に戻します。モードを変更後引き続き非標準の区切り文字を使いたい場合は，.separatorコマンドを繰り返す必要があります。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
quoteモードでは，出力はSQLリテラルとして出リクされます。文字列は一重引用符で書きまれ内部の一重引用は二つ繰り返すことでエスケープされます。Blobは16進blobリテラル表示 （例: x'abcd'）で表示されます。数はアスキーテキストでNULL値はNULLと表示されます。すべての列は互いにコンマ（あるいは.separatorが使って選択された別の文字）で区切られます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode quote</b>
sqlite&gt; <b>select * from tbl1;</b>
'hello',10
'goodbye',20
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
lineモードでは，データベースのひとつの行の各列はそれ自体が一つの行で表示されます。各行は行の名前，等号，列のデータにより構成されます。連続したレコードは空行で区切られます。lineモードの出力の例は次の通りです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode line</b>
sqlite&gt; <b>select * from tbl1;</b>
one = hello
two = 10

one = goodbye
two = 20
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
columnモードでは，各レコードは個別の行で表示されデータは列で整列されます。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode column</b>
sqlite&gt; <b>select * from tbl1;</b>
one         two       
----------  ----------
hello       10        
goodbye     20        
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
既定では各列の幅は，列のヘッダ名とデータの最初の列の幅に応じて1から10文字の間で変わります。データの幅が広く収まらない場合は，はみ出した部分が省略されます。.widthドットコマンドを使って列の幅を調整できます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.width 12 6</b>
sqlite&gt; <b>select * from tbl1;</b>
one           two   
------------  ------
hello         10    
goodbye       20    
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
上の例の.widthコマンドは，最初の列の幅を12に2番目の列の幅を6にしています。他の列の幅は変更されません。.widthコマンドには，クエリ結果の幅を指定するのに必要なだけいくつでも引数を指定できます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
列の幅を0とすると列の幅は自動的に10, ヘッダの幅，データの最初の列の幅の3つの数値の最大に決まります。これにより列の幅は自動調整されます。各列の既定の幅は，自動設定される0になっています。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
列の幅に負の値を使うと，列は右寄せされます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
出力の最初の2行に表示される列のラベルは，.headerドットコマンドを使ってオン・オフができます。これまでの例では列のラベルはオンです。オフにするには次のようにします。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.header off</b>
sqlite&gt; <b>select * from tbl1;</b>
hello         10    
goodbye       20    
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
insertモードも便利な出力形式です。insertモードでは，出力はSQL INSERT文のように表示されます。insertモードを使うと，後で別のデータベースにデータを入力するために使えるテキストを生成することができます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
insertモードを使うときは，追加の引数としてデータを入力するテーブル名を与えます。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode insert new_table</b>
sqlite&gt; <b>select * from tbl1;</b>
INSERT INTO "new_table" VALUES('hello',10);
INSERT INTO "new_table" VALUES('goodbye',20);
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
最後はhtmlモードでは。このモードでsqlite3はクエリ結果をXHTMLのテーブルとして出力します。始まりの&lt;TABLE&gt;と終わりの&lt;/TABLE&gt;は書かれませんが，途中の&lt;TR&gt;，&lt;TH&gt;，&lt;TD&gt;は出力されます。htmlモードは，CGIでの利用を想定したものです。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>6. 結果をファイルに書き込む</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
既定では，sqlite3はクエリ結果を標準出力に送ります。これを変更するには.outputや.onceコマンドを使います。出力ファイルの名前を引数として.outputに与えると，その後のクエリ結果はそのファイルに書き込まれます。また.onceコマンドを.outputコマンドの代わりにつかうと出力がリダイレクトされるのは次の単一のコマンドだけで，その後はコンソールに戻ります。.outputコマンドを引数なしで使うと再び標準出力に書き込むようになります。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode list</b>
sqlite&gt; <b>.separator |</b>
sqlite&gt; <b>.output test_file_1.txt</b>
sqlite&gt; <b>select * from tbl1;</b>
sqlite&gt; <b>.exit</b>
$ <b>cat test_file_1.txt</b>
hello|10
goodbye|20
$
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.outputまたは.onceのファイル名の最初の文字がパイプ記号（|）の場合，残りの文字はコマンドとして扱われ出力はそのコマンドに送られます。この機能により，クエリ結果を簡単に別のプロセスにパイプすることができます。例えば，Macのopen -fコマンドはテキストエディタを起動し，標準入力から読んだ内容を内容を表示します。クエリ結果をテキストエディタで表示するには，次のようにすればいいでしょう。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite3&gt; <b>.once '|open -f'</b>
sqlite3&gt; <b>SELECT * FROM bigTable;</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.outputや.onceコマンドの引数に-eを与えると出力は一時ファイルに集約されシステムのテキストエディタがそのファイルに対して起動します。つまり，.once -eコマンドは.once '|open -f'と同様の結果が得られますが，システムに依存しないという利点があります。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.outputや.onceコマンドの引数に-xを与えると，集積された結果は，コンマ区切り値（Comma-Separated-Value, CSV）の一時ファイルが生成され，それに対してCSVファイルを閲覧するための既定のシステムユーティリティ（通常は表計算プログラム）が起動されます。この機能を使うと，迅速にクリエ結果を表計算に送り簡単に閲覧することができます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite3&gt; <b>.once -x</b>
sqlite3&gt; <b>SELECT * FROM bigTable;</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.excelコマンドは.once -xのエイリアスで，全く同じ動作をします。
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

<h3>6.1 ファイル入出力関数</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
コマンドラインシェルには，二つアプリケーション定義SQL関数が追加されています。ファイルの中身をテーブルの列に読み込むものと，列の内容をファイルに書き込むものとがあります。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
readfile(X) SQL関数は，Xという名前のファイルの中身全体を読み内容をBLOBで顔します。これを使うと内容をテーブルにロードできます。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>CREATE TABLE images(name TEXT, type TEXT, img BLOB);</b>
sqlite&gt; <b>INSERT INTO images(name,type,img</b>)
   ...&gt; <b>  VALUES('icon','jpeg',readfile('icon.jpg'));</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
writefile(X,Y) SQL関数はblob YをXという名前のファイルに書き込み，書き込んだバイト数を返します。この関数はテーブルの列を一つ抽出してファイルに保存するときに使います。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>SELECT writefile('icon.jpg',img) FROM images WHERE name='icon';</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
readfile(X)とwritefile(X,Y9は拡張関数であり，SQLiteライブラリの中核には組み込まれていないことに注意してください。これらのルーチンは，<a href="https://www.sqlite.org/download.html#srctree">SQLiteソースコードリポジトリ</a>内のソースファイル<a href="http://www.sqlite.org/src/artifact?ci=trunk&amp;filename=ext/misc/fileio.c">ext/misc/fileio.c</a><a href="https://www.sqlite.org/loadext.html">ロード可能拡張</a>にあります。
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

<h3>6.2 edit() SQL関数<br></h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
もうひとつCLIにあるSQL関数はedit()です。edit()は一つか二つ引数を取ります。最初の引数は値で，通常編集しようとしている大きな複数行の文字列です。二つ目の引数はテキストエディタの名前です。二つ目の引数を省略すると，VISUAL環境変数が使われます。edit()関数は最初の引数を一時ファイルに書き込み，この一時ファイルに対してエディタを起動し，エディタ終了時にファイルをメモリに再読み込みし，編集されたテキストを返します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
edit()関数は，大きなテキスト値を変更するのに使います。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>UPDATE docs SET body=edit(body) WHERE name='report-15';</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
この例では，docs.namesがreport-15である項目のdocs.bodyフィールドの中身をエディタに送ります。エディタが終了すると，結果はdocs.bodyフィールドに書き戻されます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
edit()の既定の動作はテキストエディタの起動ですが，別の編集プログラムを二つ目の引数に用いることで，画像やその他のテキストでないリソースの編集をすることができます。例えば，テーブルのフィールドに格納されているJPEG画像を変更したいときは，次のコマンドを実行します。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>UPDATE pics SET img=edit(img,'gimp') WHERE id='pic-1542';</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
編集プログラムは，閲覧するために使い，返り値を無視することもできます。例えば，上述の画像を見るだけなら次のコマンドを走らせます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>SELECT length(edit(img,'gimp')) WHERE id='pic-1542';</b>
</pre>

<!-- /wp:html -->

<!-- wp:heading -->

<h2>7. データベースのスキーマを問い合わせる</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
sqlite3プログラムは，データベースのスキーマを見るのに便利なコマンドをいくつか提供してます。これらのコマンドがすることのうち，ほかの方法でできないものは一つもありません。これらのコマンドは，純粋にショートカットとして提供されているものです。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
例えば，データベース中のテーブル一覧を見るには，.tablesを入力します。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.tables</b>
tbl1
tbl2
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.tablesコマンドはlistモードで次のクエリを実行するようなものです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>SELECT name FROM sqlite_master 
WHERE type IN ('table','view') AND name NOT LIKE 'sqlite_%'
ORDER BY 1
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
でも，.tablesコマンドにはもっと機能があります。 主データベースだけでなく，sqlite_masterテーブルに<a href="https://www.sqlite.org/lang_attach.html">アタッチ</a>されている全てのデータベースを問い合わせを行います。また出力をきれいな列に整形します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.indexesコマンドはすべてのインデックスに対して同様に動作します。.indexesコマンドに対し，テーブルの名前が引数として与えられると，そのテーブルのインデックスだけを表示します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.schemaコマンドはデータベースの完全なスキーマ，もしくはテーブルの名前を引数で与えると単一のテーブルにスキーマを表示します。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.schema</b>
create table tbl1(one varchar(10), two smallint)
CREATE TABLE tbl2 (
  f1 varchar(30) primary key,
  f2 text,
  f3 real
)
sqlite&gt; <b>.schema tbl2</b>
CREATE TABLE tbl2 (
  f1 varchar(30) primary key,
  f2 text,
  f3 real
)
sqlite&gt;
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.schemaコマンドは，およそlistモードに設定して次のクエリを入力することに相当します。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>SELECT sql FROM sqlite_master
ORDER BY tbl_name, type DESC, name
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.tablesのように，.schemaコマンドは<a href="https://www.sqlite.org/lang_attach.html">アタッチ</a>されている全てのデータベースに対するスキーマを表示します。単一の （おそらく「主」） データベースに対するスキーマをみたいときは，.schemaに引数を追加して出力を制限可能です。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.schema main.*</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.schemaコマンドに--indentオプションを使うと，様々なスキーマのCREATE文を再フォーマットを試み，人間が読みやすいように改善します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.databasesコマンドは現在接続で開かれている全てのデータベースの一覧を表示します。最低二つあります。一つは「メイン」でもともと開いたものです。もう一つは「一時用」で一時的なテーブルに使われるデータベースです。さらにATTACH文で追加されたデータベースが表示されることもあります。出力第1列はアタッチされたデータベースの名前で第2列は外部ファイルのファイル名です。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.databases</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
.fullschemaドットコマンドは，データベースのスキーマ全体を表示するという点では.schemaのように動作します。しかし，.fullschemaは統計テーブルsqlite_stat1, sqlite_stat3, sqlite_stat4が存在する場合はそれらのダンプを含みます。通常.fullschemaは，特定のクエリに対するクエリプランを厳密に再現するのにひつようなすべての情報が得られます。SQLiteのクエリプランナに関する疑わしい問題をSQLite開発チームに報告するときは，完全な.fullschemaの出力を添えて 開発者に 問題報告をするようにお願いします。sqlite_stat3とsqlite_stat4テーブルはインデックス項目のサンプルを含むので機密情報が含まれる可能性があります。内容非開示（プロプラエタリ）のデータベースの.fullschemaの出力を公衆経路で送信しないようにしてください。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>8. CSVの取り込み</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
.importコマンドを使うとCSV（comma separated value, コンマ区切り値）データをSQLiteのテーブルに取り込むことができます。.importコマンドが取る二つの引数は，CSVデータが入っているディスク上のファイル名とCSVデータを挿入するSQLiteのテーブル名です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.importコマンドを実行する前にモードをcsvにすることが重要です。これは，コマンドラインシェルが入力ファイルのテキストを別のフォーマットとして解釈しようとするのを防ぐために必要です。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.mode csv</b>
sqlite&gt; <b>.import C:/work/somedata.csv tab1</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
二つの場合を考えましょう。(1) テーブルtab1がまだ存在しない場合，(2) テーブルtab1がすでに存在する場合。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
最初のまだテーブルが存在しない場合，テーブルは自動的に作成され入力CSVの最初の行の内容がテーブルの全ての列の名前を決めるのに使用されます。つまりテーブルが存在しないとCSVファイルの最初の行は列の名前と解釈され実際のデータはCSVファイルの2行目から始まるということになります。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
2番目のテーブルが存在する場合，CSVの最初の行を含む全ての行は実際の内容であると仮定されます。CSVファイルが最初の行に列名を含む場合，その行はデータとして読み込まれテーブルに挿入されます。これを避けるには，テーブルがもともと存在しないことを確認してください。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>9. CSV書き出し<br></h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
SQLiteのテーブル（やその一部）をCSVとして書き出すには，モードをcsvにしてテーブル内の必要な行を抽出するクエリを実行するだけです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.header on</b>
sqlite&gt; <b>.mode csv</b>
sqlite&gt; <b>.once c:/work/dataout.csv</b>
sqlite&gt; <b>SELECT * FROM tab1;</b>
sqlite&gt; <b>.system c:/work/dataout.csv</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
上の例では，.header onの行により列のラベルが出力の最初の行として印字されます。これが意味するのは，生成されるCSVファイのル最初の行は列名を含むということです。列名が必要ない場合，.header offとします。（.header offの設定は既定で，前にオンにされていない場合は省略可能です。）
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.once FILENAMEの行により，クエリのすべての出力がコンソールに印字される代わりに名前を付けたファイルに行きます。上の例では，その行によってCSVの内容はC:/work/dataout.csvと名付けられたファイルに書き込まれます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
例の最後の行（.system c:/work/dataout.csv）はc:/work/dataout.csvファイルをウィンドウズでダブルクリックしたのと同様の動作をします。大抵はスプレットシートプログラムが起動してCSVファイルが表示されます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
このコマンドは書かれた通りだと，ウィンドウズのみで動作します。Mac上での同様の行は次のようになります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.system open dataout.csv</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
Linuxや他のunixシステムでは次のように入力する必要があります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.system xdg-open dataout.csv</b>
</pre>

<!-- /wp:html -->

<!-- wp:heading {"level":3} -->

<h3>9.1 Excelへの書き出し</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
表計算への書き出しを容易にするために，CLIは.excelコマンドを提供しています。このコマンドは一つのクエリの出力を受け取り，ホストコンピュータ既定のデフォルトの表計算プログラムに送ります。次のように使ってください。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; <b>.excel</b>
sqlite&gt; <b>SELECT * FROM tab;</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
上のコマンドはクエリの出力を一時ファイルに書き込み，CSVファイルに対する既定のハンドラ（通常はExcelやLibreOfficeのような優先される表計算プログラム）を起動し，一時ファイルを削除します。このコマンドは基本的には上述した一連の.csv, .once, そして.systemコマンドの簡略表記です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.excelコマンドは，まさに.once -xのエイリアスです。.onceコマンドの-xオプションにより結果をCSVとして拡張子.csvの一時ファイルに書き，システム既定のハンドラを起動します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.once -e もあり似たような動作しますが，一時ファイルの拡張子が.txtなのでシステム既定のテキストエディタが既定の表計算プログラムに代わり起動します。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>10. データベース全体をASCIIテキストファイルに変換する</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
.dumpコマンドを使うとデータベースの内容全てを一つのASCIIテキストファイルに変換できます。 このファイルは ，<strong>sqlite3</strong>にパイプすることでデータベースに逆変換できます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
データベースファイルのアーカイブコピーを作成するのに適した方法はこちらです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>$ <b>sqlite3 ex1 .dump | gzip -c &gt;ex1.dump.gz</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
このコマンドはex1.dump.gzと名付けられたファイルを生成します。このファイルは後でデータベースを再構築したり，別のマシンに引っ越したりするために必要な全てが含まれています。データベースを再構築するには，次のコマンドを打つだけです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>$ <b>zcat ex1.dump.gz | sqlite3 ex2</b>
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
テキスト形式は純粋なSQLなので，.dumpコマンドは次のようにSQLiteのデータベースを他の人気のあるSQLデータベースエンジンに書き出すときにも使えます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>$ <b>createdb ex2</b>
$ <b>sqlite3 ex1 .dump | psql ex2</b>
</pre>

<!-- /wp:html -->

<!-- wp:heading -->

<h2>11. エクステンションのロード<br></h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
.loadコマンドを使うと，新しい独自<a href="https://www.sqlite.org/c3ref/create_function.html">アプリケーション定義SQL関数</a>，<a href="https://www.sqlite.org/datatype3.html#collation">照合順序</a>，<a href="https://www.sqlite.org/vtab.html">仮想テーブル</a>，<a href="https://www.sqlite.org/vfs.html">仮想ファイルシステム</a>を実行時にコマンドラインシェルに追加可能です。まずエクステンションを （<a href="https://www.sqlite.org/loadext.html">実行時ロード可能エクステンション</a>ドキュメントに記述されている通り） DLLや共有ライブラリに変換し，次のように入力します。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; .load /path/to/my_extension
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
SQLiteはエクステンションに対し自動的に適切な拡張子を付加する（ウィンドウズでは.dll，Macでは.dylib，その他のunixシステムでは.so）をファイル名に付加します。一般的には，エクステンションの絶対パスを指定することが良い方法です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
SQLiteはエクステンションのエントリーポイントをエクステンションのファイル名から算出します。この選択を上書きするには，エクステンションの名前を.loadコマンドの第2引数をして渡してください。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
いくつかの便利なエクステンションのソースコードがSQLiteソースコードツリーの<a href="http://www.sqlite.org/src/tree?name=ext/misc&amp;ci=trunk">ext/misc</a>サブディレクトリにあります。そのまま使うこともできますし，必要とされる問題を取り扱うための独自エクステンションの基礎として使うこともできます。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>12. データベースの内容の暗号化ハッシュ<br></h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
.sha3sumドットコマンドは，データベースの内容の<a href="https://en.wikipedia.org/wiki/SHA-3">SHA3</a>ハッシュを計算します。ハッシュはデータベースの内容に対して計算され，ディスク上での表現に対してではないことを明記しておきます。これが意味することは，例えばVACUUMや類似のデータ保存変換はそのハッシュを変更しないということです。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.sha3sumコマンドは，--sha3-224, --sha3-256, --sha3-384, --sha3-512オプションをサポートし，どのSHA3の派生型を用いるか指定できます。既定はSHA3-256です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
（<a href="https://www.sqlite.org/fileformat2.html#sqlite_master">sqlite_master</a>テーブルの）データベースのスキーマは通常ハッシュに含まれませんが，--schemaオプションを追加すれば含めることもできます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.sha3sumコマンドは一つの任意引数<a href="https://www.sqlite.org/lang_expr.html#like">LIKE</a>パターンを取ります。この引数があると名前が<a href="https://www.sqlite.org/lang_expr.html#like">LIKE</a>パターンに整合するものだけがハッシュになります。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.sha3sumコマンドは，コマンドラインシェルに含まれるエクステンション関数<a href="https://www.sqlite.org/src/file/ext/misc/shathree.c">sha3_query()</a>関数を使って実装されています。<br>
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>13. データベース内容の自己テスト</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
.selftestコマンドは，データベースが完全で壊れてないことを検証します。.selftestコマンドは，selftestという名前で次のように定義されたスキーマを探します。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>CREATE TABLE selftest(
  tno INTEGER PRIMARY KEY,  -- Test number
  op TEXT,                  -- 'run' or 'memo'
  cmd TEXT,                 -- SQL command to run, or text of "memo"
  ans TEXT                  -- Expected result of the SQL command
);
</pre>

&lt;
<!-- /wp:html -->

<!-- wp:paragraph -->
.selftestコマンドはselftest.tno順にselftestテーブルの行を読みます。各memo行に対して，このコマンドはcmdの文字列を出力に書き出します。runの各業に対して，cmdの文字列をSQLとして実行し結果をansの値と比較し，結果が異なる場合はエラーメッセージを表示します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
selftestテーブルが存在しない場合，.selftestコマンドは<a href="https://www.sqlite.org/pragma.html#pragma_integrity_check">PRAGMA整合性検査</a>を実行します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.selftest --initコマンドは，既存のものがなければselftestテーブルを作成し，全てのテーブルの内容のSHA3ハッシュを検査する項目を追加します。その後の.selftestを実行するとデータベースが何らかの形で変更されていないか検証します。一部のテーブルが変更されていないか確認するテストを生成するには，.selftest --initを実行した後，一定ではないテーブルを参照するselftestの行を<a href="https://www.sqlite.org/lang_delete.html">DELETE</a>します。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2 id="archive">14. SQLiteアーカイブ (archive)</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
.archiveドットコマンドと-Aコマンドラインオプションにより，<a href="https://www.sqlite.org/sqlar.html">SQLiteアーカイブ形式</a>を扱うことができます。インターフェースはunixシステムのtarコマンドのものに類似しています。それぞれの.arコマンド呼び出しには，必ずコマンドオプションを一つ指定しなければなりません。.archiveには，次のコマンドがあります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<table striped="1" style="margin:1em auto; width:80%; border-spacing:0">
  <tr style="text-align:left"><th style="width:15ex">オプション</th><th style="width:17ex">長いオプション</th><th>目的
  </th></tr><tr style="text-align:left;background-color:#DDDDDD"><td>-c</td><td>--create</td><td>指定したファイルを含んだ新しいアーカイブを作成する。
  </td></tr><tr style="text-align:left"><td>-x</td><td>--extract</td><td>指定したファイルをアーカイブから抽出する。
  </td></tr><tr style="text-align:left;background-color:#DDDDDD"><td>-t</td><td>--list</td><td>アーカイブ内のファイルを列挙する。
  </td></tr><tr style="text-align:left"><td>-u</td><td>--update</td><td>ファイルを既存のアーカイブに追加する。
</td></tr></table>

<!-- /wp:html -->

<!-- wp:paragraph -->
コマンドオプションとともに，それぞれの.ar呼び出しには修飾オプションを一つ以上指定することが可能です。修飾オプションは引数を取るものと取らないものとがあります。以下の修飾オプションがあります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<table striped="1" style="margin:1em auto; width:80%; border-spacing:0">
  <tr style="text-align:left"><th style="width:15ex">オプション</th><th style="width:17ex">長いオプション</th><th>目的
  </th></tr><tr style="text-align:left;background-color:#DDDDDD"><td>-v</td><td>--verbose</td><td>処理に伴って個々のファイルを列挙する。
  </td></tr><tr style="text-align:left"><td>-f FILE</td><td>--file FILE</td><td>指定すると，ファイルFILEをアーカイブとして用いる。さもなくば，現在のmainデータベースを操作の対象とする。 </td></tr><tr style="text-align:left;background-color:#DDDDDD"><td>-a FILE</td><td>--append FILE</td><td>--file同様，ファイルFILEをアーカイブとして用いるが，そのファイルを<a href="https://sqlite.org/src/file/ext/misc/appendvfs.c">apndvfs VFS</a>を用いて開き，FILEが既存の場合はアーカイブがFILEの末尾に追加されるようにする。
</td></tr><tr style="text-align:left"><td>-C DIR</td><td>--directory DIR</td><td>指定すると，全てのディレクトリを現在の作業ディレクトリではなくDIRに対する相対パスとして扱う。</td></tr><tr style="text-align:left;background-color:#DDDDDD"><td>-n</td><td>--dryrun</td><td>アーカイブ操作を実行するために走らせるSQLを表示するが，実際には何も変更しない。</td></tr><tr style="text-align:left"><td>--</td><td>--</td><td>以降全てのコマンドラインの入力はコマンド引数とし，オプションとしない。</td></tr></table>

<!-- /wp:html -->

<!-- wp:paragraph -->
コマンドラインで使う場合は，短い形式のコマンドラインオプションを-Aに続いて途中のスペースをつけずに追加します。以降全ての引数は，.archiveコマンドの一部とみなされます。例えば，次の二つのコマンドは等価です。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite3 new_archive.db -Acv file1 file2 file3
sqlite3 new_archive.db ".ar -cv file1 file2 file3"
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
長い形式と短い形式のオプションは混ぜて使えます。例えば，次の二つは等価です。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre><i>-- Two ways to create a new archive named "new_archive.db" containing</i>
<i>-- files "file1", "file2" and "file3".</i>
.ar -c --file new_archive.db file1 file2 file3
.ar -f new_archive.db --create file1 file2 file3
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
あるいは，.arに続く最初の引数は，必要な全てのオプション（-は省略）を短い形式でつなげることもできます。この場合，必要な引数は次のコマンドラインから読み込まれ，残りの語はコマンド引数とみなされます。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre><i>-- Create a new archive "new_archive.db" containing files "file1" and</i>
<i>-- "file2" from directory "dir1".</i>
.ar cCf dir1 new_archive.db file1 file2 file3
</pre>

<!-- /wp:html -->

<!-- wp:heading {"level":3} -->

<h3>14.1 SQLiteアーカイブ作成 (create) コマンド</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
新しいアーカイブを（現在のmainデータベースあるいは--fileオプションで指定されたファイルに）作成し，既存のアーカイブは上書きされます。オプションに続く各引数は，アーカイブに追加するファイルです。ディレクトリは再帰的に取り込まれます。上の例を参照してください。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

<h3>14.2 SQLiteアーカイブ抽出 (extract) コマンド</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
アーカイブからファイルを（現在の作業ディレクトリか--directoryで指定したディリクトリに）抽出します。オプションに対する引数がない場合は，全てのファイルがアーカイブから抽出されます。一方，引数が与えられた場合は，引数はアーカイブから抽出するファイル名です。指定された全てのディレクトリは再帰的に抽出されます。指定されたファイルのいずれかがアーカイブに含まれない場合はエラーになります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre><i>-- Extract all files from the archive in the current "main" db to the</i>
<i>-- current working directory. List files as they are extracted. </i>
.ar --extract --verbose

<i>-- Extract file "file1" from archive "ar.db" to directory "dir1".</i>
.ar fCx ar.db dir1 file1
</pre>

<!-- /wp:html -->

<!-- wp:heading {"level":3} -->

<h3>14.3 SQLiteアーカイブ列挙 (list) コマンド</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
アーカイブの内容を列挙します。引数なしの場合は，全てのファイルが列挙されます。引数を与えると与えものだけが列挙されます。現在，--verboseオプションは，このコマンドの動作を変更しません。この仕様は将来変更される可能性があります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre><i>-- List contents of archive in current "main" db.</i>.
.ar --list
</pre>

<!-- /wp:html -->

<!-- wp:heading {"level":3} -->

<h3>14.4 SQLiteアーカイブ更新 (update) コマンド</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
このコマンドは--createコマンドと同様に動作しますが，最初に現在のアーカイブを削除しません。ファイルの新しい版が既存の同じ名前のファイルと黙示的に置き換えられますが，そのほかは（既に存在する場合）アーカイブの内容は変更されません。
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->

<h3>14.5 ZIPアーカイブに対する操作</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
FILEがSQLiteではなくZIPアーカイブの場合でも，.archiveコマンドと-Aコマンドラインオプションは動作します。これは<a href="https://www.sqlite.org/zipfile.html">zipfile</a>エクステンションで実現されています。次のコマンドはおよそ等価で，出力の整形のみ異なります。
<!-- /wp:paragraph -->

<!-- wp:html -->

<table striped="1" style="margin:1em auto; width:80%; border-spacing:0">
  <tr style="text-align:left"><th>従来のコマンド</th><th>等価なsqlite3.exeのコマンド
  </th></tr><tr style="text-align:left;background-color:#DDDDDD"><td>unzip archive.zip</td><td>sqlite3 -Axf archive.zip
  </td></tr><tr style="text-align:left"><td>unzip -l archive.zip</td><td>sqlite3 -Atvf archive.zip
  </td></tr><tr style="text-align:left;background-color:#DDDDDD"><td>zip -r archive2.zip dir</td><td>sqlite3 -Acf archive2.zip dir
</td></tr></table>

<!-- /wp:html -->

<!-- wp:heading {"level":3} -->

<h3>14.6 SQLiteアーカイブ操作を実装しているSQL</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
様々なSQLiteアーカイブコマンドはSQL文を使って実装されています。アプリケーション開発者は，適切なSQLを走らせることでSQLiteアーカイブの読み書き機能を自分のプロジェクトに簡単に追加できます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->

<!-- /wp:paragraph -->

<!-- wp:paragraph -->
どのSQL文を使ってSQLiteアーカイブ操作が実装されているかを確認するには，--dryrunまたは-nオプションを追加してください。するとSQLが表示されますが，実行は抑制されます。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
SQLiteアーカイブ操作を実装するために用いられているSQL文は，様々な<a href="https://www.sqlite.org/loadext.html">ロード可能エクステンション</a>を利用しています。これらのエクステンションは<a href="https://sqlite.org/src">SQLiteソースツリー</a>の<a href="https://sqlite.org/src/file/ext/misc">ext/misc/ subfolder</a>にあります。SQLiteアーカイブの全ての機能を使うために必要なエンステンションは次の通りです。
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->

<ol><li><a href="https://sqlite.org/src/file/ext/misc/fileio.c">fileio.c</a>&nbsp;—&nbsp;このエクステンションは，ディスク上のファイルから中身を読み書きするSQL関数readfile()とwritefile()を追加します。fileio.cエクステンションには，ディレクトリの中身を列挙するfsdir()テーブル値関数とstat()システムコール空の数値st_mode整数をls -lコマンドのような人間が読める文字列に変換するlsname()も含まれています。</li><li><a href="https://sqlite.org/src/file/ext/misc/sqlar.c">sqlar.c</a>&nbsp;—&nbsp;このエクステンションは，SQLiteアーカイブにファイルの内容を挿入する際の圧縮，アーカイブから抽出する際の解凍に必要なsqlar_compress()はsqlar_uncompress()関数を追加します。</li><li><a href="https://www.sqlite.org/zipfile.html">zipfile.c</a>&nbsp;—&nbsp;このエクステンションが実装しているのはzipfile(FILE)テーブル値関数であり，ZIPアーカイブを読むのに使われます。このエクステンションはSQLiteアーカイブではなくZIPアーカイブを読む場合にのみ必要となります。</li><li><a href="https://sqlite.org/src/file/ext/misc/appendvfs.c">appendvfs.c</a>&nbsp;—&nbsp;このエクステンションが実装しているのは新しい<a href="https://www.sqlite.org/vfs.html">VFS</a>であり，SQLiteデータベースを実行可能ファイルのような別のファイルに付加することを可能にします。このエクステンションは.archiveコマンドの--appendオプションを用いるときだけに必要となります。</li></ol>

<!-- /wp:list -->

<!-- wp:heading -->

<h2>15. インデックスの推奨（SQLite expert）</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
<strong>注: このコマンドは試験的です。削除される可能性，あるいは将来のある時点から非互換となるような使い方の変更があり得ます。</strong>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
ほとんどの本格的なSQLデータベースにおいて，性能の鍵は正しいSQLインデックスの作成です。この文脈で「正しいSQLインデックス」はアプリケーションが必要なクエリの動作速度が最適化されるものを指しています。.expertコマンドは，特定のクエリに対しデータベースに存在すれば高速化されるであろうインデックスを提案することにより，最適化を支援するものです。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sqlite&gt; CREATE TABLE x1(a, b, c);                  <i>-- Create table in database </i>
sqlite&gt; .expert
sqlite&gt; SELECT * FROM x1 WHERE a=? AND b&gt;?;        <i>-- Analyze this SELECT </i>
CREATE INDEX x1_idx_000123a7 ON x1(a, b);

0|0|0|SEARCH TABLE x1 USING INDEX x1_idx_000123a7 (a=? AND b&gt;?)

sqlite&gt; CREATE INDEX x1ab ON x1(a, b);             <i>-- Create the recommended index </i>
sqlite&gt; .expert
sqlite&gt; SELECT * FROM x1 WHERE a=? AND b&gt;?;        <i>-- Re-analyze the same SELECT </i>
(no new indexes)

0|0|0|SEARCH TABLE x1 USING INDEX x1ab (a=? AND b&gt;?)
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
上の例では，ユーザはデータベースのスキーマ（一つのテーブルx1）を作成し，.expertコマンドを使ってクエリ SELECT * FROM x1 WHERE a=? AND b&gt;? を解析しています。シェルツールはユーザに新しいインデックス（x1_idx_000123a7）を作成することを提案し，クエリが利用しうるプランを<a href="https://www.sqlite.org/eqp.html">EXPLAIN QUERY PLAN</a>形式で出力します。そしてユーザは投下のスキーマでインデックスを作成し，同じクエリに対して再び解析を実行します。今回はシェルツールは新しいインデックスを何も提案せず，既存のインデックスを使ってクエリに対してSQLiteが使用するプランを出力します。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
.expertコマンドは次のオプションを受け付けます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<table striped="1" style="margin:1em auto; width:80%; border-spacing:0">
<tr style="text-align:left"><th> オプション</th><th>目的</th></tr><tr style="text-align:left;background-color:#DDDDDD"><td> --verbose 
    </td><td>存在すれば，解析された各クエリに対するより詳しい報告を出力する。</td></tr><tr style="text-align:left"><td> --sample&nbsp;PERCENT 
    </td><td> 既定では.expertコマンドはクエリとデータベースのスキーマだけに基づいたインデックスを推奨する。これはユーザが<a href="lang_analyze.html">ANALYZE</a>コマンドをデータベースに対して実行しデータ分布統計を生成していない場合<a href="optoverview.html">SQLite query planner</a>がクエリに対するインデックスを選択する方法に類似している。  
         <div style="margin-top:1ex">
        一つでも引数をつけて実行すると，.expertコマンドは，各データベースのテーブルに現在格納されている行のパーセントPERCENTに基づき，類似のデータ分布統計をインデックスに対して生成する。異常なデータ分布をしているデータベースに対しては，改善された推奨インデックスが得られ，特にアプリケーションがANALYZEの実行を予定してれば効果が大きい。
         <div style="margin-top:1ex">
         小さいデータベースと最近のCPUでは，--sample 100を渡す理由はない。しかし大きなデータベースに対するデータ分布統計の収集は重い処理となる可能性がある。処理が遅すぎる場合は，--sampleオプションに小さい値を与えてみるとよい。
</div></div></td></tr></table>

<!-- /wp:html -->

<!-- wp:paragraph -->
この節で説明した機能は，他のツールや<a href="http://www.sqlite.org/src/dir?ci=trunk&amp;name=ext/expert">SQLite expertエクステンション</a>を使ったツールに組み込むことができます。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>16. その他のドットコマン</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
以上の他にドットコマンドが多数コマンドラインシェルには用意されています。.helpコマンドを使うと，SQLiteの特定のバージョンやビルドに備わっているものが全て列挙されます。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>17.シェルスクリプトにおけるsqlite3の使用</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
sqliteをシェルスクリプトの中で使う一つの方法は，echoやcatを使って一連のコマンドをファイルに生成し，sqlite3を起動して生成されたコマンドファイルから入力をリダイレクトすることです。この方法は問題なく動作し，多くの場合で適切です。しかし，さらに便利にするため，sqlite3にはコマンドラインに入力する単一のSQLコマンドを2番目の引数としてデータベース名に続いて入力できます。sqlite3プログラムが二つの引数で起動されるときは2番目の引数はSQLiteライブラリに渡されて処理が実行され，クエリ結果はlistモードで標準出力に印字されてプログラムが終了します。このメカニズムは，sqlite3をawkのようなプログラムと一緒に使うのが簡単になるように設計されています。例:
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>$ <b>sqlite3 ex1 'select * from tbl1' |</b>
> <b> awk '{printf "&lt;tr&gt;&lt;td&gt;%s&lt;td&gt;%s\n",$1,$2 }'</b>
&lt;tr&gt;&lt;td&gt;hello&lt;td&gt;10
&lt;tr&gt;&lt;td&gt;goodbye&lt;td&gt;20
$
</pre>

<!-- /wp:html -->

<!-- wp:heading -->

<h2>18. シェルコマンドの終了</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
SQLiteコマンドは通常セミコロンで終わります。シェルではGO（大文字小文字を区別しない）という単語やスラッシュ文字/を行の末尾に用いてコマンドを終えることもできます。これらはSQL ServerとOracleでそれぞれ用いられているものです。これらは，<strong>sqlite3_exec()</strong>では動作しません。シェルがこれらをセミコロンに変換してから，この関数に渡しているからです。
<!-- /wp:paragraph -->

<!-- wp:heading -->

<h2>19. sqlite3プログラムのソースからのコンパイル</h2>

<!-- /wp:heading -->

<!-- wp:paragraph -->
unixシステムやWindowsのMinGWでは，いつものconfigure-makeコマンドが使えます。
<!-- /wp:paragraph -->

<!-- wp:html -->

<pre>sh configure; make
</pre>

<!-- /wp:html -->

<!-- wp:paragraph -->
configure-makeでは，ソースツリーにある素のソースからも，いろいろと追加されたバンドルからビルドできます。依存性はほとんどありません。標準的なソースからビルドするときは，動作するtclshが必要です。バンドルを使うときは，tclshで実行される全ての前処理は実行済なので通常のビルドツールだけが必要です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<a href="#archive">.archive</a>コマンドを使うには，動作する<a href="https://zlib.net/">zlib圧縮ライブラリ</a>が必要です。
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
WindowsのMSVCでは，nmakeとMakefile.mscを使います。
<!-- /wp:paragraph -->

<!-- wp:preformatted -->

<pre class="wp-block-preformatted">namke /f Makefile.msc</pre>

<!-- /wp:preformatted -->

<!-- wp:paragraph -->
.archiveコマンドが正しく動作するうに，zlibソースコードのコピーをソースツリーのcompat/zlibサブディレクトリに作成し，次のようにコンパイルしてください。
<!-- /wp:paragraph -->

<!-- wp:preformatted -->

<pre class="wp-block-preformatted">namke /f Makefile.msc USE_ZLIB=1</pre>

<!-- /wp:preformatted -->

<!-- wp:heading {"level":3} -->

<h3>19.1 自前ビルド</h3>

<!-- /wp:heading -->

<!-- wp:paragraph -->
sqlite3コマンドラインインターフェースのソースコードは，shell.cという名前の単一のファイルです。shell.cソースファイルは，他のソースから生成されますが，shell.cのほとんどはsrc/s<a href="https://sqlite.org/src/file/src/shell.c.in">https://sqlite.org/src/file/src/shell.c.in</a>hell.c.inにあります。（素のソースツリーからmake shell.cと入力するとshell.cが生成されます。）shell.c（と<a href="https://www.sqlite.org/amalgamation.html">sqlite3ライブラリのソースコード</a>）をコンパイルすると実行ファイルができます。例:
<!-- /wp:paragraph -->

<!-- wp:preformatted -->

<pre class="wp-block-preformatted"> <br>gcc -o sqlite3 shell.c sqlite3.c -ldl -lpthread -lz -lm </pre>

<!-- /wp:preformatted -->

<!-- wp:paragraph -->
コマンドラインシェルの全ての機能を使うには，次のコンパイル時オプションをつけてください。
<!-- /wp:paragraph -->

<!-- wp:html -->

<ul>
<li> <a href="compile.html#threadsafe">-DSQLITE_THREADSAFE=0</a>
</li><li> <a href="compile.html#enable_explain_comments">-DSQLITE_ENABLE_EXPLAIN_COMMENTS</a>
</li><li> <a href="compile.html#use_zlib">-DSQLITE_USE_ZLIB</a>
</li><li> <a href="compile.html#introspection_pragmas">-DSQLITE_INTROSPECTION_PRAGMAS</a>
</li><li> <a href="compile.html#enable_unknown_sql_function">-DSQLITE_ENABLE_UNKNOWN_SQL_FUNCTION</a>
</li><li> <a href="compile.html#enable_stmtvtab">-DSQLITE_ENABLE_STMTVTAB</a>
</li><li> <a href="compile.html#enable_dbpage_vtab">-DSQLITE_ENABLE_DBPAGE_VTAB</a>
</li><li> <a href="compile.html#enable_dbstat_vtab">-DSQLITE_ENABLE_DBSTAT_VTAB</a>
</li><li> <a href="compile.html#enable_offset_sql_func">-DSQLITE_ENABLE_OFFSET_SQL_FUNC</a>
</li><li> <a href="compile.html#enable_json1">-DSQLITE_ENABLE_JSON1</a>
</li><li> <a href="compile.html#enable_rtree">-DSQLITE_ENABLE_RTREE</a>
</li><li> <a href="compile.html#enable_fts4">-DSQLITE_ENABLE_FTS4</a>
</li><li> <a href="compile.html#enable_fts5">-DSQLITE_ENABLE_FTS5</a>
</li></ul>

<!-- /wp:html -->