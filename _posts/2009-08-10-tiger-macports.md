---
id: 117
title: TigerでMacPorts
date: 2009-08-10T19:52:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2009/08/10/tiger%e3%81%a7macports/'
permalink: /2009/08/10/tiger-macports/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2009/08/tigermacports.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/306887025890005421
categories:
  - コンピュータ
tags:
  - Mac
  - macports
  - Tiger
---
Mac OS X 10.4 でoctave, gnudatalanguage, ncargのコンパイルに問題があるようだ. Tigerにさらからインストールしてみる.

Ports treeはrsyncでもよいが, 更新が遅いのでここではsubversionを使うことにする. 通常はそのようにする必要はない. rsyncのports treeもしばらくすればアップデートされる

Tigerにはsubversionは入っていないので, まずsubversionをインストールする.

<pre>
sudo port -d sync
sudo port -d install subversion
</pre>

`/opt/local/etc/macports/sources.conf`を編集.

<pre>
file:///Library/MacPorts/ports [default]
</pre>
を追加し, rsyncのエントリをコメントアウト.
Ports treeを取得する.

<pre>
mkdir /Library/MacPorts/
cd /Library/MacPorts
svn checkout http://svn.macports.org/repository/macports/trunk/dports ports
</pre>

パッケージのインストール. まずはgrads.

<pre>
sudo port -d install grads
</pre>

途中でgcc43がビルドされるので時間がかかる. でも, port dependentsには出てこない. どこかでdepends_buildになっているのだろうか.
gradsの動作確認. TigerではX11は手動で起動. 環境変数の設定も必要.

<pre>
export DISPLAY=local:0.0
export GADDIR=/opt/local/share/grads
</pre>

LeopardではDISPLAYは設定しない. Xが必要になると, 自動的に起動する. ドックにX11.appをおいておく必要はないし, おくべきではない.

インストーラーでMacPortsをインストールすると, .bash_profileが書き換えられ, PATHに/opt/local/binが追加される. にもかかわらず, Tigerのxtermでは, portコマンドが見つからない. これはX11起動時も, xterm起動時も.bash_profileが読み込まれないためである. X11の「アプリケーション&gt;ターミナル&gt;メニューをカスタマイズ」の「コマンド」にオプション-lsを与える. このようにすると, xtermを起動すると, .bash_profileが読み込まれるようになる. ターミナル (Terminal.app) にはこの問題はない.

ncargは, OPeNDAP対応にするとlibmfhdf.aとlibnc-dap.dylibの_cdf_routine_nameが衝突してしまう. Nclのソースでは使っていないようだが. OPeNDAP対応のTigerバイナリはなさそうなので, うまくいかないのかもしれない. Tigerでは, OPeNDAPはあきらめ, Portfileを変更してコミットした.

今度はnclのビルドが成功し, うまくインストールできるはずである. 遠隔サーバへの接続はできないが, OPeNDAPサーバのデータが全く使えなくなる訳ではない. クイックルックにはgradsのgradsdods, あるいはgrads2のgradsdapが使える. 解析のためには, ncoのncksを使って必要な部分を切り出してダウンロードすればよい.
<pre>
sudo port -d install ncarg +g95
</pre>

ncoをインストール.

<pre>
sudo port -d install nco
</pre>

GSLをビルドするので時間がかかる.
cdoのコンパイルはすぐに終わるはずである.

<pre>
sudo port -d install cdo
</pre>

Octaveは少しPortfileに手を入れた (<a href="/2009/08/12/octave-3-2/">関連記事</a>). コミットされてからインストールした方がいいだろう. コンパイルにはかなり時間がかかる.
<pre>
sudo port -d install octave +g95
</pre>

gnudatalanguageの描画には, plplotが使われている. plplotはswigに依存しているのだが, デフォルトでたくさんのスクリプト言語に対応する. 不要な場合は, 取り除くとコンパイルが早くすむ. 特にphp5はapacheもインストールするので時間がかかる. 既にphp5などがインストールされている場合は, 取り除く必要はない.

gnudatalanguageが依存しているpython25, py25-numarrayをビルド, インストールするがあまり時間はかからない

<pre>
sudo port -d install swig -python -perl -ruby -php5
sudo port -d install gnudatalanguage +proj +g95
</pre>

gradsの代わりにgrads2でもよいかもしれない. アンサンブルに対応しているほか, Google Earthに貼るためのKMLファイルを出力できる. ncarg同様にlibnc-dapとlibmfhdfとで_cdf_routine_nameが衝突していたので, TigerではOPeNDAP非対応とした.

<pre>
sudo port -d install grads2
</pre>

grads2のコマンドには, grads-2のように-2がついている. GADDIRはgrads2用にする.

<pre>
export GADDIR=/opt/local/share/grads2
</pre>