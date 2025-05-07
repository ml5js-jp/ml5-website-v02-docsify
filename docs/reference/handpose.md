# HandPose

<center>
  <img class="header-img" src="assets/header-handpose.png" alt="HandPose Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/dinosoftlab/" target="_blank" title="DinosoftLabs">DinosoftLabs</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

## 説明

HandPoseは、ブラウザ上で手のひらの検出と手の骨格のトラッキングを可能にする機械学習モデルです。一度に複数の手を検出することができ、それぞれの手について、手のひらと指を示す21個の二次元および三次元のキーポイントを提供します。

ml5.jsのHandPoseモデルは、TensorFlow.jsの[HandPose](https://github.com/google/mediapipe/blob/master/docs/solutions/hands.md)実装に基づいています。

提供される機能:

- **手のキーポイント検出**: HandPoseは、手の21のキーポイントの二次元および三次元座標を検出できます。
- **手の左右**: HandPoseは、検出された手（左手または右手）を判定できます
- **複数の手**: HandPoseは、複数の手を同時に検出できます。

## Quick Start

構築済みの例を実行して理解しましょう！ [This HandPose example](https://editor.p5js.org/ml5/sketches/QGH3dwJ1A)のサンプルは、ウェブカメラからリアルタイムで各手の形状を表す21個の手のキーポイントを表示します。

</br>

[DEMO](iframes/handpose ":include :type=iframe width=100% height=550px")

## 例

- [HandPose Keypoints](https://editor.p5js.org/ml5/sketches/QGH3dwJ1A): ウェブカメラから検出された手のキーポイントを描画します。
- [HandPose Single Image](https://editor.p5js.org/ml5/sketches/8VK_l3XwE): 一枚の画像から手のキーポイントを検出します。
- [HandPose Parts](https://editor.p5js.org/ml5/sketches/DNbSiIYKB): 検出された手の特定の部分を描画します。
- [HandPose Start-stop](https://editor.p5js.org/ml5/sketches/W9vFFT5RM): 手の検出を開始，および停止します。

## Step-by-Step Guide

[HandPose Keypoints example](https://editor.p5js.org/ml5/sketches/QGH3dwJ1A) の製作を通じて、HandPose modelの使い方を学びましょう。

### 新しいプロジェクトを作成する

p5.js web editor で新規プロジェクトを作成します．

### ml5.jsをセットアップする

index.htmlにml5.jsをインポートします。

```html
<script src="https://unpkg.com/ml5@1/dist/ml5.js"></script>
```

?> ml5.jsライブラリのインポート方法がよくわからず、より詳細なガイダンスが必要な場合は、[Getting Started](/?id=set-up-ml5js)のページをご覧ください。

### モデルを読み込む

`sketch.js`ファイルを開き、HandPoseモデルを格納する変数を定義しましょう。

```javascript
let handPose;
```

ここで，`preload`関数でHandPoseモデルをロードします。`preload`関数を使うことで、`setup`関数と`draw`関数が呼ばれる前にモデルが読み込まれるようになります。

```javascript
function preload() {
  handPose = ml5.handPose();
}
```

### Fetch webcam videoウェブカメラの映像の取得する

ウェブカメラの映像を保存するために変数`video`を定義しよう。

```javascript
let video;
```

キャンバスの寸法を、ウェブカメラの一般的な解像度である640x480にリサイズします。

```javascript
function setup() {
  createCanvas(640, 480);
```

ウェブカメラのビデオを取得し、キャンバスに合うようにリサイズし、ディスプレイから非表示にします。

```javascript
  // Create the video and hide it
  video = createCapture(VIDEO);
  video.size(640, 480);
  video.hide();
}
```

### モデルで手のキーポイントを検出

HandPoseモデルを使用して手のキーポイントを検出する前に、検出された手を格納する変数`hands`を定義する必要があります。変数`hands`は検出された手の配列を格納します．各手はキーポイントの配列を格納する変数`keypoints`を持つことに注意してください。

```javascript
let hands = [];
```

手のキーポイントの検出を開始するには、`setup`関数の中で、`handPose`オブジェクトの`detectStart`メソッドを呼び出す必要があります。このメソッドは、入力としてウェブカメラのビデオと出力を処理するためにコールバック関数を受け取ります。

```javascript
function setup() {
  // ...
  video.hide();

  // Start detecting hands from the webcam video
  handPose.detectStart(video, gotHands);
}
```

`gotHands()` 関数は、`handPose.detectStart()` メソッドが手を検出したときに呼び出されるコールバック関数です。手が検出されると、`results`が `gotHands()` に渡され、`hands` 変数に保存されます。


```javascript
// Callback function for when handPose outputs data
function gotHands(results) {
  // Save the output to the hands variable
  hands = results;
}
```

### キャンバスにキーポイントを描画する

キーポイントを描画する前に、ウェブカメラの映像をキャンバスに描画する必要があります。

```javascript
function draw() {
  image(video, 0, 0, width, height);
```

ここで、`hands`配列をループし、検出された`i`番目の要素を取得し、`hand`変数に格納することができる。

```javascript
  // Draw all the tracked hand points
  for (let i = 0; i < hands.length; i++) {
    let hand = hands[i];
```

`i`番目に検出されたハンドのすべてのキーポイントを反復処理し、`j`番目のキーポイントを取得し、変数`keypoint`に格納する。


```javascript
    for (let j = 0; j < hand.keypoints.length; j++) {
      let keypoint = hand.keypoints[j];
```

最後に、`j`番目のキーポイントの位置に緑色の円を描く。

```javascript
      fill(0, 255, 0);
      noStroke();
      circle(keypoint.x, keypoint.y, 10);
    }
  }
}
```

検出された手（`i`は0からhandsの長さまで）のすべてのキーポイント（`j`は0からキーポイント配列の長さまで）を繰り返し処理することに注意してください。この結果、ウェブカメラのビデオで検出されたすべての手のランドマークが緑色になります。

### スケッチを実行する

ほら！これでHandPose Keypointsの例の作成は成功です。 <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `実行` 
ボタンを押して、コードの動作を確認してください。[完全なコード](https://editor.p5js.org/ml5/sketches/QGH3dwJ1A)はp5.jsウェブエディタでも見ることができます。

?> このステップ・バイ・ステップのコード・ガイドで不明な点や質問があれば、ぜひお寄せください！Discord](https://discord.com/invite/3CVauZMSt7)に参加して、どうすればもっと良くなるか教えてください。

## Properties

### handPose.model

- **Description**
  - 手のポーズ検出に使用するTensorFlow.jsモデル。
- **Type**
  - tf.LayersModel

---

### handPose.config

- **Description**
  - ユーザーがモデルに対して提供するオプション。
- **Type**
  - Object

---

### handPose.runtimeConfig

- **Description**
  - モデルの実行時の動作に関するオプション。
- **Type**
  - Object

---

### handPose.detectMedia

- **Description**
  - 手のポーズ検出を行うメディア要素（画像、ビデオ、キャンバス）。
- **Type**
  - HTMLElement

---

### handPose.detectCallback

- **Description**
  - 手のポーズ検出結果を処理するコールバック関数。
- **Type**
  - Function

---

### handPose.detecting

- **Description**
  - 検出ループが現在実行中かどうかを示すフラグ。
- **Type**
  - Boolean

---

### handPose.signalStop

- **Description**
  - 検出ループの停止を知らせるためのフラグ。
- **Type**
  - Boolean

---

### handPose.prevCall

- **Description**
  - 警告を処理するために `detectStart` または `detectStop` を呼び出したことを追跡する。
- **Type**
  - String

---

### handPose.ready

- **Description**
  - モデルがロードされたときに解決されるpromise
- **Type**
  - Promise

## Methods

### ml5.handPose()

このメソッドは、handPose オブジェクトを初期化するために使用されます。

```javascript
const handPose = ml5.handPose(?options, ?callback);
```

**Parameters:**

- **options**: オプション。 モデルのデフォルト設定を変更するオブジェクト。デフォルトで利用可能なオプションは以下の通りです。:

  ```javascript
  {
    maxHands: 2,
    flipped: false,
    runtime: "tfjs",
    modelType: "full",
    detectorModelUrl: undefined, //default to use the tf.hub model
    landmarkModelUrl: undefined, //default to use the tf.hub model
  }
  ```

  Options for hand detection:

  - _maxHands_ - オプション
    - Number: 検出する手の最大数。デフォルト：2
  - _modelType_ - オプション
    - String: 使用するモデルのタイプ： 「lite 「または 」full"。デフォルト：「full」。
  - _flipped_ - オプション
    - Boolean: 結果データを水平に反転させます。デフォルト：false。
  - _runtime_ - オプション
    モデルのランタイム： “mediapipe” または “tfjs”。デフォルトは “tfjs”。

  For using custom or offline models:

  - _solutionPath_ - オプション
    - String: モデルのファイルパスまたはURL。ランタイムが"mediapipe"の時のみ使用。
  - _detectorModelUrl_ - オプション
    - String: hand detectorモデルのファイルパスまたはURL。ランタイムが"tfjs"の時のみ使用。
  - _landmarkModelUrl_ - オプション
    - String: hand landmarkモデルのファイルパスまたはURL。ランタイムが”tfjs “の時のみ使用。

  "mediapipe"ランタイムのオプションについての詳細は[こちら](https://github.com/tensorflow/tfjs-models/tree/master/hand-pose-detection/src/mediapipe#create-a-detector)。

  "tfjs"ランタイムのオプションについての詳細は[こちら](https://github.com/tensorflow/tfjs-models/tree/master/hand-pose-detection/src/tfjs#create-a-detector。

- **callback(handPose, error)**: オプション. モデルがロードされたら実行する関数。または、p5 `preload`関数内で`ml5.handPose()`を呼び出します。

**Returns:**

- **Object**: The handPose オブジェクト。このオブジェクトは、手のポーズ検出処理を開始したり停止したりするメソッドを持っている

---

### handPose.detectStart()

このメソッドは、コールバック関数を通して画像メディア上の手の推定値を繰り返し出力する.

```javascript
handPose.detectStart(media, callback);
```

**Parameters:**

- **media**: 推定を実行するHTMLまたはp5.jsの画像、動画、またはcanvas要素
- **callback(results, error)**: 推定の出力を処理するコールバック関数。コールバック関数に渡される出力の例は以下を参照:

  ```javascript
  [
    {
      confidence,
      handedness,
      keypoints: [{ x, y, confidence, name }, ...],
      keypoints3D: [{ x, y, z, confidence, name }, ...],
      index_finger_dip: { x, y, x3D, y3D, z3D },
      index_finger_mcp: { x, y, x3D, y3D, z3D },
      ...
    }
    ...
  ]
  ```

  各キーポイントの位置は下図を参照。

  <center>
      <img alt="handPose keypoints diagram" width="600" src="assets/handpose-keypoints-map.png">
  </center>

---

### handPose.detectStop()

このメソッドは、連続的なポーズ推定プロセスを停止するために用いる。

```javascript
handPose.detectStop();
```

例えば、p5.jsのクリックイベントで手のポーズ推定を切り替えるには、この関数を次のように使います:

```javascript
// Toggle detection when mouse is pressed
function mousePressed() {
  toggleDetection();
}

// Call this function to start and stop detection
function toggleDetection() {
  if (isDetecting) {
    handPose.detectStop();
    isDetecting = false;
  } else {
    handPose.detectStart(video, gotHands);
    isDetecting = true;
  }
}
```

---

### handPose.detect()

このメソッドは、呼び出されると非同期で画像メディア上に1つの手の推定値を出力します。

```javascript
handPose.detect(media, ?callback);
```

**Parameters:**

- **media**: 推定を実行するHTMLまたはp5.jsの画像、動画、またはcanvas要素。

- **callback(results, error)**: オプション. 推定結果の出力を処理するためのコールバック関数。
