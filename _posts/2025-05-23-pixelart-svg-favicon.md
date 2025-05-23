---
category: Junk
title: ドット絵風のSVGファビコンをつくる（手動）
description: 全部手動で変換する方法です。
---

「ドット絵　SVG」で検索すると、自動で変換する内容の記事が上位に見つかりましたが、  
この記事では手動で変換していきます。


{:.no_toc}
## 目次

{:toc}
- TOC


## ドット絵を描く

<figure>
  <img src="https://res.cloudinary.com/uranuno/image/upload/v1747971505/svg-favicon-aseprite.png" alt="ドット絵エディタでガビガビのうさぎを描いているスクリーンショット" width="640" />
  <figcaption>ドット絵…？</figcaption>
</figure>

サンプルでは**Aseprite** を使用していますが、好きなツールで大丈夫です。

- [Aseprite - Animated sprite editor & pixel art tool](https://www.aseprite.org/)


## ベクターでなぞる（手動）

<img src="https://res.cloudinary.com/uranuno/image/upload/v1747971457/svg-favicon-gridsnap.png" alt="ドット絵のうさぎをパスでなぞっている（グリッドスナップON）スクリーンショット" width="640" />

サンプルでは**Inkscape** を使用していますが、好きなツールで大丈夫です。  

- [Inkscape - Draw Freely. \| Inkscape](https://inkscape.org/)

目的のアイコンのサイズでキャンバスを作成（この記事では `32 x 32 px` ）、  
下絵に先ほど描いたドット絵の画像を配置して、  
**グリッドスナップをON**にしてなぞっています。


### パスを複合化する（手動）

<figure>
  <img src="https://res.cloudinary.com/uranuno/image/upload/v1747971505/svg-favicon-compound.png" alt="path1 とpath2 を並べたスクリーンショット" width="640" />
  <figcaption>複合化して2つまで減らしたパス（見やすいよう横に並べています）</figcaption>
</figure>

なぞった後、同じ色ごとにパスを複合化しておくと、SVGのコードも減るし、  
ダークモードで別の色をあてたい時なんかにやりやすくなるかもしれません。

- [SVGファビコンのカラーをダークモード時にCSSで変更できるの知ってた？ \| コリス](https://coliss.com/articles/build-websites/operation/work/svg-favicon-in-dark-mode.html)


## SVGで書き出す

Inkscape では「名前を付けて保存→ファイルの種類：最適化SVG」でSVGを書き出します。

<figure>
  <img src="https://res.cloudinary.com/uranuno/image/upload/v1747971505/svg-favicon-export.png" alt="出力オプションスクショ XML宣言除去、viewBox有効、2スペースインデント、xml:space除去" width="400" />
  <figcaption>Inkscape の最適化SVG出力オプション</figcaption>
</figure>

```xml
<!-- Created with Inkscape (http://www.inkscape.org/) -->
<svg version="1.1" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
  <path d="m4 13v-8h2v-2h4v1h2v1h1v4h3v-6h1v-1h6v1h1v3h1v5h3v1h1v4h1v4h-1v4h-1v1h-2v1h-1v1h-3v2h-5v1h-8v-1h-2v-1h-1v-2h-2v-1h-1v-1h-1v-2h-1v-6h1v-2h1v-1z" fill="#414141"/>
  <path d="m18 3v1h-1v6h-5v-4h-1v-1h-2v-1h-2v2h-2v8h-1v1h-1v2h-1v4h1v2h1v1h1v1h2v2h1v1h2v1h6v-1h5v-2h3v-1h1v-1h2v-1h1v-4h1v-2h-1v-4h-1v-1h-3v-5h-1v-3h-1v-1zm0 11h6v6h-2v-1h-1v-4h-3zm-9 1h3v6h-2v-1h-1v-3h-3v-1h3zm8 7h2v1h-2z" fill="#fdfdfd"/>
</svg>
```

上記は書き出したSVGです。554バイトでした。  
問題なさそうのでこのまま使用します！

もしツールによって、最適化されたSVGを書き出すオプションが無い場合は、  
SVGO などを使用するとよいかもしれません。

- [svg/svgo: ⚙️ Node.js tool for optimizing SVG files](https://github.com/svg/svgo)
- [jakearchibald/svgomg: Web GUI for SVGO](https://github.com/jakearchibald/svgomg)


## 設定する

作成したアイコンをHTMLで設定します。

```html
<link rel="icon" href="/favicon.ico" sizes="32x32">
<link rel="icon" href="/favicon.svg" sizes="any" type="image/svg+xml">
```

- [2025年版、ファビコン画像の作成方法と設置方法、さまざまなデバイスに対応させるには3つのアイコンが必要 \| コリス](https://coliss.com/articles/build-websites/operation/work/how-to-favicon.html)

### ICOファイルも書き出しておく

上記で `.svg` と一緒に `.ico` も設定しています。  
2025年現在、主にSafari がSVGファビコンに対応していないためです 😠 

元のドット絵を描いたツールで `.ico` （か `.png` ）も書き出しておき、それを使用します。


## 完成

Chrome やSafari などのブラウザで確認して、  
タブにアイコンが表示されていれば完成です！

<figure>
  <img src="https://res.cloudinary.com/uranuno/image/upload/v1747971504/svg-favicon-tab.jpg" alt="スクリーンショット" width="800" />
  <figcaption>タブレットのChrome のタブ一覧表示</figcaption>
</figure>
