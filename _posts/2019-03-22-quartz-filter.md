---
title: QuartzフィルタでPDFを圧縮
date: 2019-03-22T21:15:08+09:00
author: takeshi
layout: post
permalink: /2019/03/22/quartz-filter/
categories:
  - pdf
  - mac
---
Quartzフイルタは，GhostScriptや[pdfsizeopt](/2012/04/24/pdf-compression/)を使った方法よりも，品質やサイズ，速度で有利。

Macではプレビューのファイル>書き出す...のダイアログで，フォーマット: PDF，Quartzフィルタ: Reduce File Sizeを選ぶと，ファイルサイズを小さくすることができる。
ファイルサイズはかなり小さくなるが，画像が圧縮しすぎで粗くなる。
ほどほどに圧縮するには次のようにする。

Reduce File Sizeは，Quartzフィルタの一つで`/System/Library/Filters/Reduce File Size.qfilter`にある。コピーを`~/Library/Filters`に保存する。

* 圧縮率（Compression Quality）を上げる（0〜1, 例: 0.75）。
* 縮尺率（ImageScaleFactor）を大きくする（0〜1, ColorSyncユーティリティは0〜100%）。
* 解像度（ImageResolution）を設定する（dpi, 例: 50あるいは300）。
* 画像の最大サイズ（ImageSizeMax）と最小サイズ（ImageSizeMin）を大きくする（ピクセル, 例: 2048と1024）。

ColorSyncユーティリティでも同じことができる。

JavaScriptやPython, automatorを使って，コマンドラインからQuartzフィルタを適用することもできる。

### 参考
* [How to decrease .pdf size without losing quality](https://apple.stackexchange.com/questions/297417/how-to-decrease-pdf-size-without-losing-quality)

* [「Quartzフィルタ」でPDFをコンパクトに](https://news.mynavi.jp/article/osxhack-183/)
* [quartzfilter.js](https://gist.github.com/jrk/7eb26c9a868039c70bb9)
* [PDFSuite](https://github.com/benwiggy/PDFsuite)
* [quartzfilter: Command not found](https://discussions.apple.com/thread/2790637)
