# PLATEAU SDK for Unity GIS Sample

![](./ReadmeImages/ScreenShotDay.png)

## 概要
[PLATEAU SDK for Unity](https://github.com/Project-PLATEAU/PLATEAU-SDK-for-Unity) および [PLATEAU SDK Toolkits for Unity](https://github.com/Project-PLATEAU/PLATEAU-SDK-Toolkits-for-Unity) のサンプルです。  
次の機能をデモンストレーションします。  
- PLATEAU SDK for Unityを利用し、PLATEAUの属性情報を可視化します。
  - このサンプルでは、SDKで読み取った属性情報の文字表示、また色分けによる視覚化を行います。
- PLATEAU SDK Toolkits for Unity (Map Toolkit) のGIS読込機能を利用し、国土数値情報を可視化します。
  - このサンプルでは、宙に浮かぶ文字等により路線名、公園名、学校名とその位置を表示します。
- PLATEAU SDK Toolkits for Unity (Rendering Toolkit) の機能を利用し、建物の見た目を向上します。
  - このサンプルでは、同機能により時間(昼と夜)や天候を切り替えできます。
  - 夜に設定すると、建物の窓などが光り、夜景を再現します。
- 遠景の景観表示機能はCesiumによるものです。

![](./ReadmeImages/ScreenShotNight.png)

## サンプルの利用方法
### サンプルの開き方
#### ビルド済みのアプリを利用する場合
- [リリースページ](https://github.com/Project-PLATEAU/PLATEAU-SDK-for-Unity-GISSample/releases)からアプリケーションをダウンロードできます。
#### プロジェクトファイルを利用する場合
- 本GitHubからUnityプロジェクトをダウンロードし、Unity 2022.3.25f1 で開きます。
- シーンファイル `Assets/GISSample/GISSampleScene`を開き、再生することでサンプルを実行できます。

### 操作方法と画面の説明
- 画面下の「昼夜切替」ウィンドウについて、スライダーを左端に動かすと0時になり、中央は正午、右端は24時になります。
- 画面左のウィンドウはメニューであり、情報の可視化について設定できます。
  - 「フィルタリング」では、高さやLODが指定の範囲内にある建物のみを表示し、他を非表示にできます。
  - 「天候」では雨、雪、雲を設定できます。
  - 「色分け」ではPLATEAUの属性情報を色分けで可視化します。
    - 「高さ」は属性情報から建物の高さを取得して建物を色分けします。
    - 「浸水ランク」では、浸水想定時のランクを色分けして表示します。
    - データの無い箇所は色分けされません。
- 画面右のウィンドウには、クリックした地物のPLATEAU属性情報が表示されます。
  - なお、画面にはPLATEAUのモデルとCesiumのモデルが両方表示されますが、  
    クリック可能なのは緑色の半透明の壁の範囲内であるPLATEAUのモデルのみです。
- 宙に浮かぶ文字ウィンドウは、国土数値情報を可視化したものです。  
  画面左のメニューの「空中文字の表示切替」ボタンから表示を切り替えることができます。
- 画面左のメニューの「テクスチャ表示切替」ボタンからテクスチャの表示・非表示を切り替えることができます。
- カメラは移動可能です。画面右下の「操作方法」ボタンをクリックするとカメラの操作方法が表示されます。
- カメラの位置は画面左のメニューから保存・復元できます。
  - カメラ位置の保存スロットは3つあり、「名前変更」ボタンからスロットの名前変更をできます。
  - この保存はアプリケーションを終了しても維持されます。
- 画面右下の「人のアイコン」ボタンをクリックすることで、歩行者視点に切り替わります。
  - 画面中央下に歩行者視点での操作方法が表示されます。
  - 再度アイコンをクリックすることで、俯瞰視点に戻ります。

![](./ReadmeImages/ScreenShotWalk.png)

- 画面右下の「車のアイコン」ボタンをクリックすると、車両視点モードに切り替わります。
  - 対象となる車両はランダムに選ばれます。
  - もう一度アイコンをクリックすると、俯瞰視点に戻ります。
  - また、走行中の車両をクリックすることで、選択した車両の視点に切り替えることができます。

![](./ReadmeImages/ScreenShotCar.png)

## サンプルの仕組み
- 近景には属性情報を含むPLATEAU都市モデルがあります。  
  PLATEAUの属性情報はシーンにコンポーネントとして配置され、PLATEAU SDKによって読みこまれることで  
  クリックでの属性表示や色分けを実装しています。
- 時間や天候の変更機能は、PLATEAU SDK Toolkits for Unityの機能の1つである、  
  Rendering Toolkitの「環境システムの設定」によるものです。
- 夜にすると建物の窓等が光り輝く機能は、Rendering Toolkitの「自動テクスチャ生成」によるものです。
- 空中に浮かぶ文字で路線名、公園名、学校名が表示されるのは、国土数値情報を元にしています。  
  国土数値情報などGISデータは、Toolkitsの機能の1つであるMaps Toolkitの「GISデータ読み込み」によるものです。
- 遠景の表示にはCesiumを利用しています。
- 道路の生成には、PLATEAU SDKの機能の1つである、道路ネットワークの「道路生成」を利用しています。
- 車両の走行には、PLATEAU SDK Toolkit for Unityの機能の1つである、「交通シュミレーション機能」を利用しています。
- 樹木や看板などのアセットの配置には、PLATEAU SDK Toolkit for Unityの機能の1つである、「アセット配置機能」を利用しています。

## 別の都市モデルでサンプルを実行したい場合
- シーンに配置済みの千代田区の都市モデルを削除し、代わりにお好みの都市モデルをPLATEAU SDKでインポートします。
- 都市モデルをGISサンプル向けに自動設定するために次の手順に従います。
  - CityAdjusterを任意のゲームオブジェクトにアタッチし、インスペクタから都市モデルを選択してExecボタンを押します。
  
## ライセンス
- 本リポジトリのライセンスは[LICENSE.md](./LICENSE.md)をご参照ください。
- 本システムの開発は株式会社シナスタジアが行っています。
- ソースコードおよび関連ドキュメントの著作権は国土交通省に帰属します。

## 注意事項
- 本リポジトリの内容は予告なく変更・削除する可能性があります。
- 本リポジトリの利用により生じた損失及び損害等について、国土交通省はいかなる責任も負わないものとします。
