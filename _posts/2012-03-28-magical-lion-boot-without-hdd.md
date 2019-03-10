---
id: 61
title: 起動ディスクを抜いても起動したLionの魔法
date: 2012-03-28T18:32:00+09:00
author: takeshi
layout: post
guid: 'https://www.enomosphere.net/2012/03/28/%e8%b5%b7%e5%8b%95%e3%83%87%e3%82%a3%e3%82%b9%e3%82%af%e3%82%92%e6%8a%9c%e3%81%84%e3%81%a6%e3%82%82%e8%b5%b7%e5%8b%95%e3%81%97%e3%81%9flion%e3%81%ae%e9%ad%94%e6%b3%95/'
permalink: /2012/03/28/magical-lion-boot-without-hdd/
blogger_blog:
  - hiyokoz.blogspot.com
blogger_author:
  - Takeshi
blogger_permalink:
  - /2012/03/lion.html
blogger_internal:
  - /feeds/832545220475396382/posts/default/1118860870836923233
categories:
  - コンピュータ
tags:
  - Lion
  - Mac
---
仕事のメインマシンであるMac Proは，いつからかファイル共有もリモートログインもできなくなった．共有はもちろんオンだし，ファイアウォールも使っていない．hosts.allowを書いてみたりして，tcpwrapperを起動させたりしたのがいけなかったのかもしれないが，結局よく分からない．セーフモードで起動して，Mac OS X 10.7.3 comboを再適用したがこれもだめ．Lionの再インストールを決断した．
でも，バックアップは面倒なのでこの機会に起動ディスクを大きいもの（2TB）に入れ替えることにした．Mac Proのディスク交換は至って簡単．蓋を開けてディスクトレイを引き出す．ディスクを入れ替えて戻す．電源を入れる．
こんなときのために，あらかじめ用意しておいたインストールDVDで起動しなくてはと思っていたが，起動中はWireless Keyboardが認識されずディスクのトレイが空かない．USBキーボードを探しているうちに，なんとLionのインストーラが起動していた．OSの入っているハードディスクもDVDもUSBドライブもないはずだ．魔法だ！
ちゃんと確認していないが，どうやよTime Machineとして使っている2番目のディスクの隠しボリュームから起動したようだ．それにしても起動ディスクを空のディスクに入れ替えたのに起動するのには驚いた．
OSのインストール中に追加コンポーネントをダウンロードしていたのだが，起動してみると最新のMac OS X 10.7.3になっている．これまでの常識では，OSを入れ替えたらアップデートしなければならなかった．
iOSばかり注目されているが，Mac OS Xも心地よい進化を遂げている．

追記: diskutil listしても、起動ドライブ以外にはApple_Boot Recovery HDはないので、<a href="http://support.apple.com/kb/HT4718?viewlocale=ja_JP">インターネット復元</a>のだろうと思います。