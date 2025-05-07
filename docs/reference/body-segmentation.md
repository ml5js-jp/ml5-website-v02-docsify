# 人体セグメンテーション

<center>
  <img class="header-img" src="assets/header-body-segmentation.png" alt="BodySegmentation Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/ibrandify/" target="_blank" title="ibrandify">ibrandify</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

## 説明

Ml5.jsの人体セグメントには、`SelfieSegmentation`と`BodyPix`という2つのモデルがある。`SelfieSegmentation`は、背景から被写体をセグメントする（領域を分割する）ことに重点を置いています。`BodyPix`は、主に画像や動画における体の部位のセグメント（異なる手足の区別など）に使用される。BodyPix は人物と背景の分割も実行できますが、計算量が多くなります。

ml5.jsのBodySegmentationは、[TensorFlow.jsのBodyPixとMediaPipeのSelfie Segmentation](https://github.com/tensorflow/tfjs-models/tree/master/body-segmentation)を用いて構築されています。

提供される機能:
- **リアルタイムの人物/背景セグメンテーション**: `SelfieSegmentation`モデルは、リアルタイムで背景から人物をセグメントすることができ、軽量に設計されている。`BodyPix`モデルもこの目的に使用できるが、計算量が多くなる
- **リアルタイムに身体部位の検出**: `BodyPix` モデルは、24 の身体部位をリアルタイムでセグメントできます。

## Quick Start

このサンプルプログラムでは，[BodySegmentation `BodyPix`](https://editor.p5js.org/ml5/sketches/ruoyal-RC)を用いて，ウェブカメラの映像から身体部位をセグメントします

</br>

[DEMO](iframes/body-segmentation ":include :type=iframe width=100% height=550px")

## 例
- [BodySegmentation Mask Body Parts](https://editor.p5js.org/ml5/sketches/ruoyal-RC): ウェブカメラの映像から体の部位をセグメントする

- [BodySegmentation Mask Background](https://editor.p5js.org/ml5/sketches/KNsdeNhrp): ウェブカメラの映像から背景をセグメントする
- [BodySegmentation Mask Person](https://editor.p5js.org/ml5/sketches/h6TN8umP5): ウェブカメラの映像から人をセグメントする

## Step-by-Step Guide

[BodySegmentation Mask Body Part](https://editor.p5js.org/ml5/sketches/ruoyal-RC)の制作を通じて，BodySegmentation model の使い方を学びまょう．


### 新しいプロジェクトを作成する

To follow along, start by creating an empty project in the [p5.js web editor](https://editor.p5js.org/).

### ml5.jsをセットアップする

`index.html`にml5.jsをインポートします。

```html
<script src="https://unpkg.com/ml5@1/dist/ml5.js"></script>
```

?> ml5.jsライブラリのインポート方法がよくわからず、より詳細なガイダンスが必要な場合は、[Getting Started](/?id=set-up-ml5js)のページをご覧ください。

### modelを読み込む
`sketch.js`ファイルを開き、BodySegmentationモデルを格納する変数を定義ましょう。


```javascript
let bodySegmentation;
```

ここでは、ウェブカメラの入力から体のパーツを分割したいので，optionsオブジェクトでマスクの種類を`parts`に指定しよう。

```javascript
let options = {
  maskType: "parts",
};
```

?> オプションオブジェクトでマスクタイプを `person` または `background` に指定することもできます。オプションオブジェクトの詳細については、[Methods](/reference/body-segmentation?id=methods) セクションを参照してください。

それでは、BodySegmentationモデルを指定されたオプションでプリロードしてみよう。`preload`関数を使うことで、`setup`関数や`draw`関数が呼ばれる前にモデルが読み込まれるようになります。

```javascript
function preload() {
  bodySegmentation = ml5.bodySegmentation("BodyPix", options);
}
```

### ウェブカメラの映像の取得

ウェブカメラの映像を扱うために，変数`video`を定義しよう

```javascript
let video;
```

キャンバスの寸法を、ウェブカメラの一般的な解像度である640x480にリサイズする．

```javascript
function setup() {
  createCanvas(640, 480);
```

ウェブカメラのビデオを取得し、キャンバスに合うようにサイズを変更し、ディスプレイから非表示にします。

```javascript
  // Create the video and hide it
  video = createCapture(VIDEO);
  video.size(640, 480);
  video.hide();
}
```

### modelで体の部位を検出する
BodySegmentation モデルを使って、ウェブカメラの入力から体のパーツを検出できる。セグメンテーションされた体のパーツを保存する、変数`segmentation`を定義しよう。


```javascript
let segmentation;
```

体のパーツの検出をするには、`setup`関数の中で、`bodySegmentation`オブジェクトの`detectStart`メソッドを呼び出す必要があります。このメソッドは、ウェブカメラのビデオと，出力を処理するコールバック関数を引数として受け取ります．

```javascript
function setup() {
  // ...
  video.hide();

  // Start detecting body parts from the webcam video
  bodySegmentation.detectStart(video, gotResults);
}
```


`gotResults()` は、`bodySegmentation.detectStart()` メソッドがボディパーツを検出したときに呼び出されるコールバック関数です。ボディパーツが検出されると、`result`が `gotResults()` に渡され、`segmentation`に保存されます。

```javascript
function gotResults(result) {
  segmentation = result;
}
```

?> `result` オブジェクトには追加のプロパティもあります。 出力オブジェクトの詳細については、[Methods](/reference/body-segmentation?id=methods) セクションを参照してください。

### セグメントされた体の部位を表示する
セグメントされた体のパーツを表示する前に、キャンバスをクリアしてウェブカメラの映像を描画しましょう。

```javascript
function draw() {
  background(255);
  image(video, 0, 0);
```

変数`segmentation`が空でなければ、セグメンテーションされたボディパーツをキャンバス上に表示することができる。

```javascript
  if (segmentation) {
    image(segmentation.mask, 0, 0, width, height);
  }
}
```

### スケッチを実行する
これで、BodySegmentation Mask Body Part のサンプルが作成できました！<img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `実行`ボタンを押して、コードの動きを見てみましょう。[完全なコード](https://editor.p5js.org/ml5/sketches/ruoyal-RC) はp5.jsウェブエディタでも見ることができます。

?> このステップ・バイ・ステップのコード・ガイドで不明な点や質問があれば、ぜひお寄せください！ [Discord](https://discord.com/invite/3CVauZMSt7)に参加して、どうすればもっと良くなるか教えてください。


## Properties

### bodySegmentation.modelName

- **Description**
  - 使用するモデルの名前。通常は "BodyPix" または "SelfieSegmentation"
- **Type**
  - String

---

### bodySegmentation.video

- **Description**
  - セグメンテーションが実行されるビデオ
- **Type**
  - HTMLVideoElement

---

### bodySegmentation.model

- **Description**
  - 身体のセグメンテーションに使用されたTensorFlow.jsモデル
- **Type**
  - tf.LayersModel

---

### bodySegmentation.config

- **Description**
  - モデルに設定可能なオプション
- **Type**
  - Object

---

### bodySegmentation.runtimeConfig

- **Description**
  - モデルの実行時の動作に関する設定オプション
- **Type**
  - Object

---

### bodySegmentation.detectMedia

- **Description**
  - 人体セグメンテーションが実行されるメディア要素（画像, 動画, キャンバス）

- **Type**
  - HTMLElement

---

### bodySegmentation.detectCallback

- **Description**
  - ボディセグメンテーションの結果を処理するコールバック関数
- **Type**
  - Function

---

### bodySegmentation.ready

- **Description**
  - モデルがロードされたときに解決されるpromise
- **Type**
  - Promise

---



## Methods

### ml5.bodySegmentation()

This method is used to initialize the bodySegmentation object.このメソッドは bodySegmentation オブジェクトを初期化する。

```javascript
const bodySegmentation = ml5.bodySegmentation(?modelName, ?options, ?callback);
```

**Parameters:**

- **modelName**: 使用するモデルを指定する文字列。モデルの種類:
  - _SelfieSegmentation_(default): 背景から人をセグメントするために使用するモデル
  - _BodyPix_: 人物や体の一部をセグメントするために使用できるモデル



- **options**: オプション.モデルのデフォルト設定を変更するためのオブジェクト。オプションオブジェクトの例を参照してください:

  ```javascript
  {
    runtime: "tfjs", // "tfjs" or "mediapipe"
    modelType: "general", // "general" or "landscape"
    maskType: "background", // "background", "person", or "parts" (used to change the type of segmentation mask output)
    flipped: false,
  }
  ```

  重要なオプション:
  - _maskType_: 出力するマスクのタイプ。以下オプション:
    - _background_:背景のマスク。その結果、背景が透明なピクセルで、人物が黒いピクセルの画像になる。
    - _person_:人のマスク。その結果、背景は黒いピクセルで、人物は透明なピクセルを持つ画像になる。
    - _parts_: **BodyPix** のみ.体の部分のマスク。その結果、背景が白いピクセルで、体は部位ごとにさまざまな色のピクセルで塗り分けられた画像になる
  - _flipped_ - オプション
    - Boolean: 結果を水平に反転する。デフォルトはfalse。
  
  

  [More info on options for SelfieSegmentation model with tfjs runtime](https://github.com/tensorflow/tfjs-models/tree/master/body-segmentation/src/selfie_segmentation_tfjs#create-a-detector).

  [More info on options for SelfieSegmentation model with mediaPipe runtime](https://github.com/tensorflow/tfjs-models/tree/master/body-segmentation/src/selfie_segmentation_mediapipe#create-a-detector).

  [More info on options for BodyPix model.](https://github.com/tensorflow/tfjs-models/blob/master/body-segmentation/src/body_pix/README.md#create-a-detector)

- **callback(bodySegmentation, error)**: オプション. モデルがロードされたら実行する関数。または、p5 `preload`関数内で`ml5.bodySegmentation()`を呼び出します

**Returns:**

- **Object**: The bodySegmentation object．このオブジェクトには、ボディセグメント検出処理を開始および停止するメソッドが含まれています。

---

### bodySegmentation.detectStart()

このメソッドは、コールバック関数を通じて、画像メディア上のセグメンテーションマスクを繰り返し出力する。

```javascript
bodySegmentation.detectStart(media, callback);
```

**Parameters:**

- **media**: セグメンテーションを実行するHTMLまたはp5.jsの画像、動画、またはcanvas

- **callback(output, error)**: 設定.ボディ・セグメンテーションの結果を処理するコールバック関数。

`output`には、以下のプロパティを持つオブジェクトが含まれます。 Based on the `maskType` オプションに基づいて，`mask` （および `maskImageData`）は、検出 された背景のマスクか、検出された人物のマスクか、または検出された人物の身体部分の（色付き）マスクのいずれかを含む。


  ```javascript
  {
    mask: {}, // a p5 Image object, can be directly passed into p5 image() function
    maskImageData: {}, // the mask as an ImageData object
    data: [], // an array of raw detection results
    imageData: {}, // an ImageData object of the raw detection results
  }
  ```

`data`配列には、画像のセグメンテーション結果が含まれ、入力画像の各ピクセルに 1 つの数値として格納されます。 (BodyPixモデルでは、右手はたとえば 11 となり、 `bodySegmentation.LEFT_HAND` と同じになります。)

  _results.mask_ under different _maskType_ options:
  - _background_: 背景のマスク。results.maskは、背景に透明なピクセル、人物に黒いピクセルを持つ画像である。
  - _body_: 人物のマスク。_results.mask_ は、背景が黒ピクセル、人物が透明ピクセルの画像である。
  - _parts_: **BodyPix** のみ. _results.mask_ は、背景に白いピクセル、体の各部位に様々な色のピクセルを持つ画像である。

---

### bodySegmentation.detectStop()

このメソッドは、'bodySegmentation.detectStart'を呼び出した後に呼び出すことで、ポーズ推定の繰り返しを停止させることができる。

```javascript
bodySegmentation.detectStop();
```

---

### bodySegmentation.detect()

このメソッドは、呼び出されると非同期で画像メディアに単一のセグメンテーションマスクを出力します。

```javascript
bodySegmentation.detect(media, ?callback);
```

**Parameters:**

- **media**: セグメンテーションを実行するHTMLまたはp5.jsの画像、動画、またはcanvas

- **callback(output, error)**: オプション。 推定結果を出力を処理するためのコールバック関数。

**Returns:**
セグメンテーション出力を解決するプロミス。
