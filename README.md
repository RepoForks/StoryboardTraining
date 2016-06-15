# Storyboard Training

デザイナー向けStoryboard勉強会資料

## 事前準備

以下の作業を事前に完了させておいてください。

- Xcodeのインストール
  - どちらか好きな方でインストールしてください
     - https://itunes.apple.com/jp/app/xcode/id497799835?mt=12
     - https://developer.apple.com/downloads/
- Xcodeを1回以上起動
  - 初回起動は時間がかかります

## Storyboardとは

- アプリの画面遷移と画面レイアウトをグラフィカルに編集するためのツールです
- Xcodeで作成することができます
- `.storyboard` という拡張子のファイルで、内部的にはXMLです

## 用語

- View(ビュー)
  - 画面に表示されるパーツを意味します
  - ボタン、ラベル、画像などもViewです

- View Controller(ビューコントローラ)
  - Viewを管理する機能の集合です
  - アプリの各画面は1つ以上のView Controllerで構成されています
  - 簡単なiOSアプリの画面は、1画面=1View Controllerで構成されていることが多いです
  - 複雑な画面を構成するために、View Controllerの中にView Controllerを配置することができます
  - **Storyboard上ではScene(シーン)と呼ばれることがあります**

- Segue(セグエ)
  - あるシーンから次のシーンへのトランジション(遷移)を表します
  - Segueをカスタムすることで、画面間のデータの受け渡しを実現できます

## Xcodeプロジェクトの作成

- 新規プロジェクトを作成します
  1. File > New > Project
  1. `Choose a template for your new project:` で `Single View Application` を選択してNextボタンを押します
     - ![newpj](./images/create-xcode-project/template.png)
  1. `Choose options for your new project:` で以下のように入力して、Nextボタンを押します
     - Product Name: アプリ名
         - 今回は任意のものでOK
     - Organization Name:  開発者名
         - 今回は任意のものでOK
     - Organization identifier: 開発者を一意に識別するID ドメインを逆に並べたものを使用することが多いです
         - 今回は任意のものでOK
     - Language: 開発に使用するプログラミング言語 
         - 今回は `Swift` を選択
     - Devices: 対応する端末

     - ![newpj](./images/create-xcode-project/options.png)
  1. プロジェクトの保存先を指定してCreateボタンを押します

## Xcodeの各エリアの名称

### Window

![window](./images/xcode-area-name/window.png)

### Editor

|アイコン|名称|説明|
|:--:|:--:|:--|
|![standard-editor](./images/xcode-area-name/standard-editor.png)|Standard editor|選択したコンテンツを表示し、編集するエリアです。<br/>ショートカットキーは `Command+Enter`。|
|![assistant-editor](./images/xcode-area-name/assistant-editor.png)|Assistant editor|Standard editorに表示したコンテンツに関連するコンテンツを表示するエリアです。<br/>ショートカットキーは `Command+Option+Enter` 。<br/>また、Navigator areaで `Optionキーを押しながらコンテンツをクリック` で任意のファイルを表示することもできます。|
|![version-editor](./images/xcode-area-name/version-editor.png)|Version editor|過去のバージョンとの比較を表示するエリアです。この機能は、プロジェクトがバージョン管理されている時のみ使用可能です。<br/>ショートカットキーは `Command+Option+Shift+Enter` 。|

### Pane

![pane](./images/xcode-area-name/pane.png)

### Inspector pane

選択したファイル、オブジェクトの各種設定を表示、編集できます。

|アイコン|名称|説明|
|:--:|:--:|:--|
|![file-inspector](./images/xcode-area-name/file-inspector.png)|File inspector|選択したファイルのパスや名前などを表示、編集できます。|
|![quick-help](./images/xcode-area-name/quick-help.png)|Quick Help|選択したインタフェースのエレメントや、ファイルの詳細を表示できます。|
|![identity-inspector](./images/xcode-area-name/identity-inspector.png)|Identity inspector|オブジェクトのクラス名やRuntime attributesなどを表示、編集できます。|
|![attributes-inspector](./images/xcode-area-name/attributes-inspector.png)|Attributes inspector|選択したインタフェースオブジェクトの属性を設定できます。|
|![size-inspector](./images/xcode-area-name/size-inspector.png)|Size inspector|インタフェースオブジェクトの初期サイズ、位置などの特性を記入できます。|
|![connection-inspector](./images/xcode-area-name/connection-inspector.png)|Connections inspector|インタフェースオブジェクトのOutletやActionを表示します。また、新しいConnectionを作成したり、既存のConnectionを削除したりできます。|


### Library pane

ここからNavigator areaやEditor areaにパーツをドラッグアンドドロップして、ソースコードやインタフェースオブジェクトを追加できます。 
パレットのようなものだと思ってください。

|アイコン|名称|説明|
|:--:|:--:|:--|
|![file-templates](./images/xcode-area-name/file-templates.png)|File templates|Storyboard編集中には使いません。<br/>一般的なファイルのテンプレートです。Navigator areaにドラッグアンドドロップしてファイルを追加できます。|
|![code-snnipets](./images/xcode-area-name/code-snnipets.png)|Code snippets|Storyboard編集中には使いません。<br/>Editor areaにドラッグアンドドロップで、コードスニペットをソースコードに追加できます。|
|![objects](./images/xcode-area-name/objects.png)|Objects|**Storyboard編集中に頻繁に使います。**<br/>Editor areaにドラッグアンドドロップで、インタフェースオブジェクトをソースコードに追加できます。|
|![media](./images/xcode-area-name/media.png)|Media files|画像、アイコン、音声ファイルなどをEditor areaにドラッグアンドドロップで、nibファイルに追加できます。|

## インタフェースオブジェクトの作成

### ラベルの作成

ラベルは文字を表示するインタフェースオブジェクトです。 
画面内にラベルを作成し、任意の文字列を表示してみましょう。

1. Navigator areaでMain.storyboardを選択します
1. Library paneのObjectsを表示します
1. `View Controller Scene` を選択します
1. `Label` を `View Controller Scene` 内にドラッグアンドドロップします
  - `View Controller Scene` の左上の方に置くようにしてください
  - インタフェースオブジェクトの種類が多くて見つけにくいので、下にあるフィルタを利用すると簡単に任意のインタフェースオブジェクトを配置できます
  - ![filter](./images/create-interface-object/filter.png)
  - ![create-label](./images/create-interface-object/create-label.png)
1. 作成したラベルを選択した状態で、 `Attribute inspector` を表示します
1. Textの下のテキストフィールドに任意の文字列を入力します
  - ![custom-text](./images/create-interface-object/custom-text.png)
1. ↑で入力した文字列がラベル内で表示しきれない場合は、ラベルのサイズを調整します

#### やってみよう💪

1. Buttonを作成してみましょう
1. Viewを作成して、背景色を赤にしてみましょう
1. 背景が赤いViewの上にSwitchを作成してみましょう


![answer](./images/create-interface-object/answer.png)

## シミュレータの起動

- Toolbarのデバイス名が表示されている所をクリックし、任意のデバイスを選択します
  - ![run](./images/run-simulator/select-device.png)
- Runボタン![run](./images/run-simulator/run.png)を押します
  - ショートカットキーは `Command+r` です
- シミュレータが起動し、作成したインタフェースオブジェクトが表示されていれば成功です
  - シミュレータの初回の起動には時間がかかります
- Hardware > Rotate Left および Rotate Right で画面を回転できます
  - ショートカットキーは　`Command+←` および `Command+→` です

![simulator](./images/run-simulator/simulator.png)

## Debug View Hierarchy

- シミュレータ起動中にDebug areaの ![button](./images/debug-view-hierarchy/button.png) ボタンを押します
- Viewの階層が3D表示されます

![hierarchy](./images/debug-view-hierarchy/hierarchy.png)

## Storyboard Preview

毎回シミュレータを起動するのは大変なので、レイアウトの確認にはStoryboardのPreview機能が便利です。

- Assistant editorを表示します
- Automaticと表示されている部分をクリックし、 Preview > Main Storyboard(Preview) を選択します
  - ![preview](./images/storyboard-preview/select-preview.png)
- Assistant editorの左下の `+` をクリックし任意のデバイスを選択します
  - 複数のデバイスでのレイアウトを同時に確認できます

![preview](./images/storyboard-preview/preview.png)

## Navigationbar

画面にNavigationbarを追加します

- `View Controller Scene` を選択します
- Editor > Embed In > Navigation Controller
  - ![navigationbar](./images/navigationbar/navigationbar.png)
- シミュレータやStoryboard Previewでレイアウトを確認します


## Autolayout

### 概要

[Auto Layoutガイド：Auto Layoutの概要](https://developer.apple.com/jp/documentation/UserExperience/Conceptual/AutolayoutPG/index.html) 
Safariで閲覧すること

### 一緒にやろう👟

![pranctice1](./images/autolayout/practice1.png)

### やってみよう💪

1. 全画面でマージンなしの水色のViewを作ってみましょう
1. Auto Layoutガイドの等幅のビューを作ってみましょう
1. 幅が異なる2つのビューを作ってみましょう
1. 等間隔に横に並ぶ3つのピンク色のビューを作ってみましょう
  - 3つのビューの横幅と縦幅は50ポイントに固定です
  - 左右のビューは画面左右端から0ポイントの位置にあります

### Leran more

- [Auto Layoutの設計ベストプラクティスと、Viewの種類ごとのテクニック集 - Qiita](http://qiita.com/yuya_presto/items/08b0656f67a59c8c2d03)

## Asset Catalog

- [About Asset Catalogs](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/chapters/Recipe.html)

## Segue

## Storyboardファイルの作成

- 一番上のグループを右クリック > New File...

## Storyboard Reference

## コードとのひも付け

## Runtime Attributes

## IB Designable and Inspectable

## 参考資料

- [About the Utilities Area](https://developer.apple.com/library/ios/recipes/xcode_help-general/Chapters/AbouttheUtilityArea.html)
- [Storyboard Help](https://developer.apple.com/library/ios/recipes/xcode_help-IB_storyboard/_index.html#//apple_ref/doc/uid/TP40014225)
- [Xcode Overview: Designing with Storyboards](https://developer.apple.com/library/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/DesigningwithStoryboards.html#//apple_ref/doc/uid/TP40010215-CH43-SW1)
- [2つ目のiOSアプリケーション：ストーリーボード (TP40011318 0.0.0) - SecondiOSAppTutorial.pdf](https://developer.apple.com/jp/documentation/SecondiOSAppTutorial.pdf)
- [Auto Layoutガイド (TP40010853 0.0.0) - AutolayoutPG.pdf](https://developer.apple.com/jp/documentation/AutolayoutPG.pdf)
- [Auto Layoutガイド：Auto Layoutの概要](https://developer.apple.com/jp/documentation/UserExperience/Conceptual/AutolayoutPG/index.html)
- [About Asset Catalogs](https://developer.apple.com/library/ios/recipes/xcode_help-image_catalog-1.0/chapters/Recipe.html)
- [今度こそ克服するAutoLayoutの使い方・基礎編～SwiftからはじめるiOSアプリ開発:その5【初心者向けアプリ開発3分tips】 - エンジニアtype](http://type.jp/et/log/article/ra-ios-tips06)