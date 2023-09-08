---
category: Demonstration
title: ローカルでビルドして表示確認するための記事
---

css を変更する際にUIの組み合わせでどのように見えるか確認したいので、スタイルを作成したUI をすべて含む記事を用意しておきます。

_draft に入れておき、実際のビルドには含まれないようにします。

1. TOC
{:toc}

## 目次
目次は☝のように表示されます。

## 記事内の一番大きな見出しはH2
記事内の一番大きな見出しはH2 を使用する想定です。

H1 もスタイルは用意していますが、記事タイトルと同じフォントサイズに設定してあり、基本的に使わないと思います。

### その次に大きな見出しH3
H3 くらいまでは、まあ使うかな？

## コードブロック
```html
<html>
  <head>
  </head>
  <body>
    <p>Hello, World!</p>
  </body>
</html>
```

ちなみにインラインコードは `<!-- こんな感じ -->` です。

## 箇条書き
- ひとつ目の項目
  - 小項目
- ふたつ目の項目
- みっつ目の項目

1. ひとつ目の項目
2. ふたつ目の項目
3. みっつ目の項目
  - 小項目
  - インデントの幅が意図通りか確認してください

## リンク
[文中のリンク](/)はこんな感じです。

### リンクカード
カードのようにリンクを表示するスタイルも作りました。

サイト名は2行、URL は1行より長くなると省略されるので、複数のカードが並んだ時にカードの高さが揃うようになっています。 

[**GitHub**](https://github.com/)

[**GitHub Pages サイトの Jekyll ビルドエラーに関するトラブルシューティング - GitHub Docs**](https://docs.github.com/ja/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites)

```markdown
<!-- サイト名は強調しないと省略が効かないので注意 -->
[**サイト名**](url)
```

がんばって作ったけど使うかな・・・

## 注意書き

{:.note}
注意書きがあればこんな感じで表示できます。  
改行を含むことも、  
[リンク](/)を含むことも可能です。

## 画像

![Octocat]{:width="400" height="400"}

![アス比を指定したり、figcaption を書いたりもできます][Octocat]{:standalone width="400" .ar-3-2}

[Octocat]: /assets/images/github-pages/octocat.png

```markdown
<!-- 画像の高さは指定した方が良いらしいです -->
![Image]{:width="400" height="400"}

<!-- アス比は固定数値のクラスを作ってあるのでそれを指定します -->
![キャプション][Image]{:standalone width="400" .ar-3-2}

[Image]: /assets/images/hogehoge.jpg

```

- [aspect-ratio - CSS: カスケーディングスタイルシート \| MDN](https://developer.mozilla.org/ja/docs/Web/CSS/aspect-ratio)
- [Setting Height And Width On Images Is Important Again — Smashing Magazine](https://www.smashingmagazine.com/2020/03/setting-height-width-images-important-again/)

## 引用
> Markdown（マークダウン）は、文書を記述するための軽量マークアップ言語のひとつである。本来はプレーンテキスト形式で手軽に書いた文書からHTMLを生成するために開発されたものである。しかし、現在ではHTMLのほかパワーポイント形式やLATEX形式のファイルへ変換するソフトウェア（コンバータ）も開発されている。各コンバータの開発者によって多様な拡張が施されるため、各種の方言が存在する。

[Markdown - Wikipedia](https://ja.wikipedia.org/wiki/Markdown) より

## 水平線
使用頻度は低そうですが、H2 用に角丸の破線をsvg で作ったので・・・

* * *

・・・流用して作りました。
