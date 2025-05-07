# BodyPose

<center>
  <img class="header-img" src="assets/header-bodypose.png" alt="BodyPose Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/sentyairma1/" target="_blank" title="sentya irma">sentya irma</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

## 概要

<!--
The ml5.js BodyPose is a pretrained full-body pose estimation model that can estimate poses and track key body parts in real-time. It is developed leveraging TensorFlow's [MoveNet](https://www.tensorflow.org/hub/tutorials/movenet#:~:text=MoveNet%20is%20an%20ultra%20fast,known%20as%20Lightning%20and%20Thunder) and [BlazePose](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) models.
-->
ml5.jsのBodyPoseは、事前学習された全身のポーズ推定モデルです。このモデルはポーズ推定と、リアルタイムに身体の主要部位を追跡することができます。これはTensorFlowの[MoveNet](https://www.tensorflow.org/hub/tutorials/movenet#:~:text=MoveNet%20is%20an%20ultra%20fast,known%20as%20Lightning%20and%20Thunder)や[BlazePose](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker)モデルを活用して開発されました。また、TensorFlowとは、画像認識・音声認識、翻訳、自然言語処理などで活用される、Googleが開発した機械学習のオープンソースライブラリです。

<!--
It offers flexibility for:
-->
以下のような柔軟性を提供します：

<!--
- **Multi-person detection**: Estimate poses for single or multiple people in the frame.
- **Video and image inputs**: Estimate poses from both images and live or recorded videos.
- **Choose between two models**: MoveNet (17 keypoints, optimized for speed) and BlazePose (33 keypoints, optimized for precision).
-->
- **複数人検出**: フレーム内の単一または複数人のポーズを推定します。
- **動画や画像の入力**: 画像と、ライブまたは録画映像の両方からポーズを推定します。
- **2つのモデルから選択**: MoveNet(17のキーポイントを持つ、速度に最適化されたモデル)やBlazePose(33のキーポイントを持ち、精度に最適化されたモデル)から選択できます。

<!--
## Quick Start
-->
## クイックスタート!

<!--
Run and explore a pre-built example! [This bodyPose example](https://editor.p5js.org/ml5/sketches/hMN9GdrO3) uses the MoveNet model to detect body poses in real-time from the webcam 
video.
-->
事前に構築されたサンプルを実行して見てみましょう！ [このbodyPoseのサンプル](https://editor.p5js.org/ml5/sketches/hMN9GdrO3)は、ウェブカメラ映像からリアルタイムに身体ポーズを検出するMoveNetモデルが使用されています。
</br>

[DEMO](iframes/bodypose ":include :type=iframe width=100% height=550px")

<!--
## Examples
-->
## サンプル

<!-- ### p5 sketches

- [BodyPose MoveNet Keypoints](https://editor.p5js.org/ml5/sketches/hMN9GdrO3): Draw the keypoints of the detected body using MoveNet model.
- [BodyPose BlazePose keypoints](https://editor.p5js.org/ml5/sketches/OukJYAJAb): Draw the keypoints of the detected body using BlazePose model.
- [BodyPose Skeletal Connections](https://editor.p5js.org/ml5/sketches/YBuqxIH1S): Draw the skeletons on poses for the MoveNet model.

### Video Tutorials

- [Pose Estimation with ml5.js](https://thecodingtrain.com/tracks/ml5js-beginners-guide/ml5/7-bodypose/pose-detection) by The Coding Train -->

### p5 sketches

- [BodyPose MoveNet キーポイント](https://editor.p5js.org/ml5/sketches/hMN9GdrO3)：MoveNetモデルを使って検出された身体のキーポイントを描画。
- [BodyPose BlazePose キーポイント](https://editor.p5js.org/ml5/sketches/OukJYAJAb)：BlazePoseモデルを使って検出された身体のキーポイントを描画。
- [BodyPose Skeletal Connections](https://editor.p5js.org/ml5/sketches/YBuqxIH1S): MoveNetモデルで検出したポーズに骨格を描く。

### Video Tutorials

- [Pose Estimation with ml5.js](https://thecodingtrain.com/tracks/ml5js-beginners-guide/ml5/7-bodypose/pose-detection) by The Coding Train

<!--
## Step-by-Step Guide
-->
## 段階的なガイド

<!--
Now, let's together build the [BodyPose Keypoints example](https://editor.p5js.org/ml5/sketches/hMN9GdrO3) from scratch, and in the process, learn how to use the BodyPose model.
-->
それでは一緒にBodyPose Keypoints exampleをゼロから構築しましょう！その過程で、BodyPoseモデルの使い方を学ぶことができます！

<!--
### Create a new project
-->
### 新しいプロジェクトを作成する

<!--
To follow along, start by creating an empty project in the [p5.js web editor](https://editor.p5js.org/).
-->
[p5.js web エディター](https://editor.p5js.org/)で空のプロジェクトを作成することから始めましょう！

<!--
### Set up ml5.js
-->
### ml5.jsのセットアップ

<!--
Import the ml5.js library in your `index.html` file by copying the following `<script>` tag.
-->
以下の`<script>` タグをコピーし、`index.html`ファイルにml5.jsライブラリをインポートします。


```html
<script src="https://unpkg.com/ml5@1/dist/ml5.js"></script>
```

<!--
?> If you are not familiar with how to import the ml5.js library and need more detailed guidance, please check out our [Getting Started](/?id=set-up-ml5js) tutorial.
-->
?>もし、ml5.jsライブラリのインポート方法がわからず、より詳細なガイダンスが必要であれば、[Getting Started](/?id=set-up-ml5js)チュートリアルをご覧ください。


<!--
### Load model
-->
### モデルをロードする

<!--
Open the `sketch.js` file. Define a variable to hold the bodyPose model.
-->
Sketch.jsファイルを開いてください。bodyPoseモデルを保持する変数を定義します。

```javascript
let bodyPose;
```

<!--
Create a `preload()` function to load the bodyPose model.
-->
bodyPoseモデルをロードするためのpreload()関数を作成します。 


```javascript
function preload() {
  // Load the bodyPose model
  bodyPose = ml5.bodyPose();
}
```

<!--
?> You can also pass a model name, an options object, and a customized callback function to the `ml5.bodyPose()` function (e.g., `ml5.bodyPose("BlazePose", options, modelLoaded)`) to change the default configuration of the model. For more information on the available configuration settings, refer to the [Methods](/reference/bodypose?id=ml5bodypose) section on this page.
-->
?>モデルのデフォルト設定を変更するために、`ml5.bodyPose()`関数にモデル名やオプションオブジェクト、カスタマイズしたコールバック関数を渡すこともできます。</br>（例：`ml5.bodyPose("BlazePose", options, modelLoaded)`）利用可能な設定のより詳しい情報については、このページの[Methods](/reference/bodypose?id=ml5bodypose)セクションを参照してください。


<!--
### Fetch webcam video
-->
### ウェブカメラ映像を取得

<!--
Define a variable `video` to hold the webcam video.
-->
ウェブカメラの映像を保持するために、変数videoを定義します。

```javascript
let video;
```

<!--
Resize the canvas dimensions to 640x480, a common resolution for webcams.
-->
キャンバスのサイズを、ウェブカメラの一般的な解像度である640x480にリサイズします。

```javascript
function setup() {
  createCanvas(640, 480);
```

<!--
Fetch the webcam video, resize it to fit the canvas, and hide it from the display.
-->
ウェブカメラの映像を取得し、キャンバスに合うようにリサイズして、ビデオを非表示にします。

```javascript
  // Create the video and hide it
  video = createCapture(VIDEO);
  video.size(640, 480);
  video.hide();
}
```

<!--
### Detect poses
-->
### ポーズを検出する

<!--
Define a variable `poses` to hold the detected poses.
-->
ポーズ検出を保持するために変数`poses`を定義します。


```javascript
let poses = [];
```

<!--
To start detecting poses in the webcam video, call the `bodyPose.detectStart()` method. Here, we pass two parameters: the webcam video and a customized callback function `gotPoses`.
-->
ウェブカメラ映像でポーズ検出を開始するためには、`bodyPose.detectStart()`メソッドを呼び出します。ここでは、ウェブカメラの映像(video)とカスタマイズされたコールバック関数`gotPoses`の2つのパラメータを渡します。


```javascript
function setup() {
  // ...
  video.hide();

  // Start detecting poses in the webcam video
  bodyPose.detectStart(video, gotPoses);
}
```

<!--
The `gotPoses()` function is a callback function that will be called when the `bodyPose.detectStart()` method detects poses. Once the poses are detected, the output `results` will be passed to `gotPoses()`, and then saved to the `poses` variable.
-->
`gotPoses()`関数は、`bodyPose.detectStart()`メソッドがポーズを検出した時に呼び出されるコールバック関数です。ポーズが検出されると、出力の`results`は`gotPoses()`に渡され、そして変数`poses`に保存されます。

```javascript
// Callback function for when the model returns pose data
function gotPoses(results) {
  // Store the model's results in a global variable
  poses = results;
}
```

<!--
### Draw skeleton on the canvas
-->
### キャンバスに骨格を描画する

<!--
We can draw the skeleton by connecting the keypoints of the detected poses with lines. To achieve this, we first need to understand which keypoints are connected to each other. Define a variable `connections` to hold the skeleton connections.
-->
検出されたポーズのキーポイントを線で繋げることで、骨格を描画することができます。これを実現するために私たちは、どのキーポイントが互いに接続されているかを最初に理解する必要があります。骨格の接続を保持するために変数`connections`を定義します。


```javascript
let connections;
```
<!--
Use `bodyPose.getSkeleton()` in the `setup()` function to get the connections between keypoints. This method returns an array of arrays, where each sub-array contains the indices of the connected keypoints. For example, `[[0, 1], [0, 2], ...]` means that keypoints 0 (Nose) and 1 (Left Eye) are connected, keypoints 0 (Nose) and 2 (Right Eye) are connected, and so on.
-->
キーポイント間の接続を取得するために、`setup()`関数で `bodyPose.getSkeleton()`を使います。このメソッドは、２次元配列を返し、配列の中の配列（これ以降サブ配列とする）は、接続されたキーポイントのインデックスが格納されています。例えば、 [[0, 1], [0, 2], ...] は、キーポイント0（鼻）と1（左目）が接続されたこと、キーポイント0（鼻）と2（右目）が接続されたことを意味します。その他の場合でも同様にして接続を確認することができます。
```javascript
function setup() {
  // ...
  bodyPose.detectStart(video, gotPoses);
  // Get the skeleton connection information
  connections = bodyPose.getSkeleton();
}
```

<!--
In the `draw()` function, draw the webcam video on the canvas.
-->
`draw()`関数では、キャンバスにウェブカメラ映像を描画します。


```javascript
function draw() {
  // Display the video
  image(video, 0, 0, width, height);
```
<!--
Next, we can start drawing the skeleton connections. We iterate through the `poses` array, where each object `pose` is a pose of a person, containing an array of `keypoints`. Each `keypoint` object has the properties `x`, `y`, and `confidence`. The `confidence` is the confidence score of the keypoint prediction (a number between zero and one).
-->
次に、身体の骨組みを描画します。`poses`という配列を使って、各人物のポーズ情報を処理します。この`pose`は1人分のポーズ情報を持っていて、その中には`keypoints`という配列があります。`keypoints`の各オブジェクトには、体の部位ごとの位置情報`x`、`y`と、その部位がどれだけ正確に検出されたかを示す信頼度スコア情報`confidence`（0から1の間を取る）が入っています。

```javascript
  // Draw the skeleton connections
  for (let i = 0; i < poses.length; i++) {
    let pose = poses[i];
```

<!--
Within each pose, we only want to draw the skeleton connections that the model has a high confidence in predicting. To do this, we need to check for each link in the `connections` array and whether the `keypoints` that constitute the link have a `confidence` score greater than 0.1. If they do, we draw a line connecting the keypoints.
-->
各ポーズの中で、モデルが高い信頼度で予測している身体の骨組みのみを描画します。そのためには、`connections`配列内の各接続を確認します。接続している`keypoints`が、`confidence`スコア0.1を超えていた場合、そのキーポイント同士を繋ぐ線を描きます。
<!--
各ポーズの中で、モデルが高い信頼度で予測している身体の骨組みのみを描画したいです。これをするためには、connections配列内の各リンクを確認し、そのリンクを構成するkeypointsが、0.1より大きいconfidenceスコアであるどうかを確認する必要があります。
-->

<!--
We iterate through the connections array, with each item being a link of `pointA` and `pointB`. For instance, `connections[1]` is `[0, 2]`, where 0 is the index of `pointA` and 2 is the index of `pointB`. Thus, `let pointAIndex = connections[j][0];` means we get the starting point (pointA) of the link `j`, and `let pointBIndex = connections[j][1];` means we get the ending point (pointB) of the link `j`.
-->
`connections`配列を順番に処理していきます。この配列の各要素は、`pointA`と`pointB`をつなぐ接続を表しています。例えば、`connections[1]`が`[0, 2]`の場合、0は `pointA`のインデックスで、2は`pointB`のインデックスです。つまり、`let pointAIndex = connections[j][0];`は接続`j`の開始点（pointA）のインデックスを取得することを意味し、`let pointBIndex = connections[j][1];`はその接続の終了点（pointB）のインデックスを取得することを意味します。要するに、検出された骨組みの線の始点と終点のインデックスを取得するということです。

<!--
Use the indices to retrieve the `pointA` and `pointB` objects from the `pose.keypoints`. As with all keypoints, `pointA` is an object with properties `x`, `y`, and `confidence`.
-->
インデックスを使用して、`pose.keypoints`から`pointA`と`pointB`のオブジェクトを取得します。全てのキーポイントと同様に、`pointA`は`x`、`y`および`confidence`のプロパティを持つオブジェクトです。

```javascript
    for (let j = 0; j < connections.length; j++) {
      let pointAIndex = connections[j][0];
      let pointBIndex = connections[j][1];
      let pointA = pose.keypoints[pointAIndex];
      let pointB = pose.keypoints[pointBIndex];
```

<!--
Now, we can draw the line connecting the keypoints if both points have a confidence score greater than 0.1.
-->
始点と終点の両方の信頼度スコアが0.1以上であれば、キーポイントを結ぶ線を描画します。

```javascript
      // Only draw a line if we have confidence in both points
      if (pointA.confidence > 0.1 && pointB.confidence > 0.1) {
        stroke(255, 0, 0);
        strokeWeight(2);
        line(pointA.x, pointA.y, pointB.x, pointB.y);
      }
    }
  }
```

<!--
### Draw keypoints on the canvas
-->
### キャンバスにキーポイントを描画する

<!--
We can also represent each of the keypoints on the canvas. To do this, we will iterate through the `poses` array and draw a circle for each keypoint if the confidence score is greater than 0.1.
-->
各キーポイントもキャンバス上に表示することができます。dこれを行うためには、`poses`配列を反復処理し、信頼度スコアが0.1より大きい場合は、各キーポイントに円を描画します。

<!--
We can get each person's pose from the `poses` array. Each `pose` object contains an array of `keypoints`.
-->
`poses`配列から人のポーズを取得することができます。各`pose`オブジェクトは`keypoints`の配列が含まれています。

```javascript
  // Iterate through all the poses
  for (let i = 0; i < poses.length; i++) {
    let pose = poses[i];
```

<!--
Next, we iterate through all of the keypoints in `keypoints`.
-->
次に、`keypoints`配列内の全てのキーポイントを順番に処理します。

```javascript
    // Iterate through all the keypoints for each pose
    for (let j = 0; j < pose.keypoints.length; j++) {
      let keypoint = pose.keypoints[j];
```

<!--
For each keypoint, we only want to draw a circle if the keypoint's confidence is greater than 0.1. We can use the `confidence` property of the keypoint object to check the confidence score.
-->
各キーポイントについて、信頼度が0.1より大きい場合のみ円を描画します。キーポイントオブジェクトの`confidence`プロパティを使うことで、信頼度スコアを確認することができます。


```javascript
      // Only draw a circle if the keypoint's confidence is greater than 0.1
      if (keypoint.confidence > 0.1) {
        fill(0, 255, 0);
        noStroke();
        circle(keypoint.x, keypoint.y, 10);
      }
    }
  }
}
```

<!--
### Run your sketch
-->
### スケッチを実行する

<!--
Voila! You have successfully built the BodyPose model to detect and draw body poses in real-time from the webcam video. Press the <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `run` button to see the code in action. You can also find the [complete code](https://editor.p5js.org/ml5/sketches/hMN9GdrO3) in the p5.js web editor.
-->
できました！BodyPoseモデルの構築に成功しました！このモデルは、ウェブカメラの映像からリアルタイムに身体ポーズを検出して描画します。<img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `実行`ボタンを押してコードの動作を見てみましょう。[完全なコード](https://editor.p5js.org/ml5/sketches/hMN9GdrO3)はp5.jsウェブエディターでも確認できます。


<!--
?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better.
-->
?> この段階的なコードガイドで質問や不明点がございましたら、ぜひご連絡ください。[Discord](https://discord.com/invite/3CVauZMSt7)に参加して、改善点をお知らせください。

<<<<<<< HEAD

<!--
## Properties
-->
## プロパティ

### bodyPose.modelName

<!--
- **Description**
  - The name of the model being used, either "MoveNet" or "BlazePose".
- **Type**
  - String
-->
- **説明**
  - 使用するモデルの名前。「MoveNet」または「BlazePose」のいずれかを使用する。
- **型**
  - String
---

### bodyPose.model

<!--
- **Description**
  - The TensorFlow.js model used for pose detection.
- **Type**
  - tf.LayersModel
-->
- **説明**
  - ポーズ検出に使用されるTensorFlow.jsモデル。
- **型**
  - tf.LayersModel
---

### bodyPose.runtimeConfig

<!--
- **Description**
  - Configuration options related to the runtime behavior of the model.
- **Type**
  - Object
-->
- **説明**
  - モデルの実行時に関する設定。
- **型**
  - Object

---

### bodyPose.detectMedia

<!--
- **Description**
  - The media element (image, video, or canvas) on which pose detection is performed.
- **Type**
  - HTMLElement
-->
- **説明**
  - ポーズ検出が実行されるメディア要素（画像、映像、またはキャンバス）。
- **型**
  - HTMLElement
---

### bodyPose.detectCallback

<!--
- **Description**
  - The callback function to handle pose detection results.
- **Type**
  - Function
-->
- **説明**
  - ポーズ検出結果を処理するコールバック関数
- **型**
  - Function
---

### bodyPose.detecting

<!--
- **Description**
  - A flag indicating whether the detection loop is currently running.
- **Type**
  - Boolean
-->
- **説明**
  - 検出ループが現在実行中かどうかを示すフラグ
- **型**
  - Boolean

---

### bodyPose.signalStop

<!--
- **Description**
  - A flag used to signal the detection loop to stop.
- **Type**
  - Boolean
-->
- **説明**
  - 検出ループの停止を知らせるためのフラグ
- **型**
  - Boolean
---

### bodyPose.prevCall

<!--
- **Description**
  - Tracks the previous call to `detectStart` or `detectStop` to handle warnings.
- **Type**
  - String
-->
- **説明**
  - `detectStart`または`detectStop`のどちらが最後に呼び出されたかを記録するプロパティ。連続した呼び出しなど不適切な状況を警告する
- **型**
  - String
---

### bodyPose.ready

<!--
- **Description**
  - A promise that resolves when the model has loaded.
- **Type**
  - Promise
-->
- **説明**
  - モデルが完全にロードされた時に解決されるPromiseという型のプロパティ。（Promise：非同期処理の結果を待つためのオブジェクト）このプロパティはモデルの準備が整ったことを知らせるために使われる。モデルが読み込まれたら、bodyPose.ready は「解決」され、指定された処理が実行される。
- **型**
  - Promise
  
<!--
=======
>>>>>>> upstream/main
## Methods
-->
## メソッド

### ml5.bodyPose()

<!--
This method is used to load the bodyPose model and store it in a variable. The `?` means the argument is optional!
-->
このメソッドは、bodyPoseモデルをロードし、変数に格納するために使用されています。`?`は、引数がオプションであることを意味しています。

<!--
TODO: Add default model name, and explain the options, callback.
-->

```javascript
let bodypose = ml5.bodyPose(?model, ?options, ?callback);
```

**Parameters:**

<!--
- **model**: Optional. Which model to use: the possible options are `MoveNet` (default) and `BlazePose`.
-->
- **model**: オプション。使用するモデルを指定する。選択肢は、`MoveNet`(デフォルト)または`BlazePose`。

<!--
- **options**: Optional. An object to change the default configuration of the model. The available options differ depending on which of the two underlying models are used.
-->
- **options**: オピション。モデルのデフォルト設定を変更するためのオブジェクト。使用可能なオプションは、どちらのモデルを使用するかによって異なる。

<!--
The default and available options are:
-->
デフォルトで使用可能なオプションは以下の通りです。

  ```javascript
  {
    modelType: "MULTIPOSE_LIGHTNING", // "MULTIPOSE_LIGHTNING", "SINGLEPOSE_LIGHTNING", or "SINGLEPOSE_THUNDER".
    enableSmoothing: true,
    minPoseScore: 0.25,
    multiPoseMaxDimension: 256,
    enableTracking: true,
    trackerType: "boundingBox", // "keypoint" or "boundingBox"
    trackerConfig: {},
    modelUrl: undefined,
    flipped: false
  }
  ```

  <!--
  Options for both models: 
  -->

  <!--
  - _modelType_ - Optional
    - String: The type of model to use. Default: "MULTIPOSE_LIGHTNING".
  - _enableSmoothing_ - Optional
    - Boolean: Whether to smooth the pose landmarks across different input images to reduce jitter. Default: true.
  - _flipped_ - Optional
    - Boolean: Flip the result horizontally. Defaults to false. 
  -->
  両方のモデルが持つオプション:

  - _modelType_ - オプション
    - String: 使用するモデルの型。デフォルトではMULTIPOSE_LIGHTNING。
  - _enableSmoothing_ - オプション
    - Boolean: Boolean:ジッターを減らすために異なる入力画像間でポーズランドマークをスムーズにするかどうか。デフォルトではtrue。
  - _flipped_ - オプション
    - Boolean: 結果を水平に反転させる。デフォルトではFalse。

  <!--
  Options for the MoveNet model only:

  - _minPoseScore_ - Optional
    - Number: The minimum confidence score for a pose to be detected. Default: 0.25.
  - _multiPoseMaxDimension_ - Optional
    - Number: The target maximum dimension to use as the input to the multi-pose model. Must be a mutiple of 32. Default: 256.
  - _enableTracking_ - Optional
    - Boolean: Track each person across the frame with a unique ID. Default: true.
  - _trackerType_ - Optional
    - String: Specify what type of tracker to use. Default: "boundingBox".
  - _trackerConfig_ - Optional
    - Object: Specify tracker configurations. Use tf.js settings by default.
  -->
  MoveNetモデルのみのオプション:
  
  - _minPoseScore_ - オプション
    - Number: ポーズを検出するための信頼度スコアの最小値。デフォルトでは 0.25
  - _multiPoseMaxDimension_ - オプション
    - Number: マルチポーズモデルの入力として使用する画像の最大サイズの目標値。32の倍数でなければならない。デフォルトでは 256.
  - _enableTracking_ - オプション
    - Boolean: フレーム内を横断する人を一意のIDで追跡するかどうか。デフォルトではtrue
  - _trackerType_ - オプション
    - String: 使用する追跡タイプを指定する。デフォルトでは"BoundingBox"
  - _trackerConfig_ - オプション
    - Object: 追跡設定を指定する。デフォルトでtf.jsの設定を使用する。

  <!--
  Options for the BlazePose model only:

  - _runtime_ - Optional
    - String: Either "tfjs" or "mediapipe". Default: "tfjs"
  - _enableSegmentation_ - Optional
    - Boolean: A boolean indicating whether to generate the segmentation mask.
  - _smoothSegmentation_ - Optional
    - Boolean: whether to filters segmentation masks across different input images to reduce jitter.
  -->
  BlazePoseモデルのみのオプション:

  - _runtime_ - オプション
    - String: : “tfjs”または“mediapipe”のどちらか。デフォルトでは "tfjs"
  - _enableSegmentation_ - オプション
    - Boolean: セグメンテーションマスクを生成するかどうか。デフォルトではfalse。
  - _smoothSegmentation_ - オプション
    - Boolean: ジッターを減らすために異なる入力画像間でセグメンテーションマスクをフィルタリングするかどうか。デフォルトではtrue。

  <!--
  For using custom or offline models

  - _modelUrl_ - Optional
    - String: The file path or URL to the MoveNet model.
  - _solutionPath_ - Optional
    - String: The file path or URL to the mediaPipe BlazePose model.
  - _detectorModelUrl_ - Optional
    - String: The file path or URL to the tfjs BlazePose detector model.
  - _landmarkModelUrl_ - Optional
    - String: The file path or URL to the tfjs BlazePose landmark model.
  -->
  カスタムモデルまたはオフラインモデルを使用する場合

  - _modelUrl_ - オプション
    - String: MoveNetモデルへのファイルパスまたはURL.
  - _solutionPath_ - オプション
    - String: mediaPipe BlazePoseモデルへのファイルパスまたはURL.
  - _detectorModelUrl_ - オプション
    - String: tfjs BlazePose検出モデルへのファイルパスまたはURL.
  - _landmarkModelUrl_ - オプション
    - String: tfjs BlazePosePランドマークモデルへのファイルパスまたはURL.

  <!--
  See See the [MoveNet documentation](https://github.com/tensorflow/tfjs-models/tree/master/pose-detection/src/movenet#create-a-detector) and the [BlazePose documentation](https://github.com/tensorflow/tfjs-models/tree/master/pose-detection/src/blazepose_tfjs#create-a-detector) for more information on available options.
  -->
使用可能なオプションの詳細な情報は[MoveNet ドキュメント](https://github.com/tensorflow/tfjs-models/tree/master/pose-detection/src/movenet#create-a-detector)ドキュメントおよび[BlazePose ドキュメント](https://github.com/tensorflow/tfjs-models/tree/master/pose-detection/src/blazepose_tfjs#create-a-detector)を参照してください。

<!--
- **callback(bodypose, error)**: Optional. A "callback" function that runs when the model has been successfully loaded. Most ml5.js example call `ml5.bodyPose()` in the p5.js `preload()` function and no callback is needed.
-->
- **callback(bodypose, error)**: オプション。モデルが正常にロードされた時に実行するコールバック関数。ほとんどのml5.jsのサンプルは、p5.jsのpreload()関数でml5.bodyPose()を呼び出しており、コールバックは必要ありません。

**Returns:**
**返り値:**

<!--
- **Object**: The bodyPose object. This object contains the methods to start and stop the pose detection process.
-->
- **Object**: bodyPoseオブジェクト。このオブジェクトはポーズ検出のプロセスを開始や停止をするメソッドを含む。

---

### bodypose.detectStart()

<!--
This method starts the pose detection process and runs it continuously on real-time video.
-->
このメソッドは検出プロセスを開始し、リアルタイム映像で継続的に実行します。

```javascript
bodypose.detectStart(media, gotPoses);
```

**Parameters:**
**パラメータ:**

<!--
- **media**: An HTML or p5.js image, video, or canvas element to run the estimation on.
- **gotPoses(results, error)**: A callback function to handle the results of the pose estimation. See below for an example of the model's results:
-->
- **media**: 推定を実行するための要素。HTMLまたはp5.js画像、映像またはキャンバス。
- **gotPoses(results, error)**: ポーズ推定の結果を処理するためのコールバック関数。モデルの結果の例については以下を参照ください：

  ```javascript
  [
    {
      box: { width, height, xMax, xMin, yMax, yMin },
      id: 1,
      keypoints: [{ x, y, confidence, name }, ...],
      left_ankle: { x, y, confidence },
      left_ear: { x, y, confidence },
      left_elbow: { x, y, confidence },
      ...
      confidence: 0.28,
    },
    ...
  ];
  ```

  <!--
  BodyPose's MoveNet model predicts a set of 17 keypoints:
  -->
  BodyPose の MoveNet モデルは一連の 17 のキーポイントを予測します。17のキーポイントを以下に示します。

  <!--
  Nose, Left Eye, Right Eye, Left Ear, Right Ear, Left Shoulder, Right Shoulder, Left Elbow, Right Elbow, Left Wrist, Right Wrist, Left Hip, Right Hip, Left Knee, Right Knee, Left Ankle, Right Ankle
  -->
  鼻、左目、右目、左耳、右耳、左肩、右肩、左肘、右肘、左手首、右手首、左股関節、右股関節、左膝、右膝、左足首、右足首 

  <!--
  See the diagram below for the position of each keypoint.
  -->
  各キーポイントの位置については、以下のダイアグラムをご参照ください。 
  <center>
      <img style="display:block; max-width:50%" alt="MoveNet keypoint diagram" src="./assets/BodyPose-MoveNet-Keypoints.png">
  </center> <br/>

  <!--
  BodyPose's BlazePose model predicts a set of 33 keypoints:
  -->
  BodyPose‘s BlazePose モデルは一連の 33 のキーポイントを予測します。33のキーポイントを以下に示します。

  <!--
  Nose, Left Eye Inner, Left Eye, Left Eye Outer, Right Eye Inner, Right Eye, Right Eye Outer, Left Ear, Right Ear, Mouth Left, Mouth Right, Left Shoulder, Right Shoulder, Left Elbow, Right Elbow, Left Wrist, Right Wrist, Left Pinky, Right Pinky, Left Index, Right Index, Left Thumb, Right Thumb, Left Hip, Right Hip, Left Knee, Right Knee, Left Ankle, Right Ankle, Left Heel, Right Heel, Left Foot Index, Right Foot Index, Body Center, Forehead, Left Thumb, Left Hand, Right Thumb, Right Hand
  -->
  鼻、左目の内側、左目、左目の外側、右目の内側、右目、右目の外側、左耳、右耳、口の左、口の右、左肩、右肩、左肘、右肘、左手首、右手首、左小指、右小指、左人差し指、右 人差し指、左親指、右親指、左股関節、右股関節、左膝、右膝、左足首、右足首、左踵、右 踵、左足指、右足指、身体の中心、額、左親指、左手、右親指、右手

  <!--
  See the diagram below for the position of each keypoint.
  -->
  各キーポイントの位置については、以下のダイアグラムをご参照ください。
  
  <center>
      <img style="display:block; max-width:50%" alt="BlazePose keypoint diagram" src="./assets/BodyPose-BlazePose-Keypoints.png">
  </center>

  ```javascript
  [
    {
      box: { width, height, xMax, xMin, yMax, yMin },
      id: 1,
      keypoints: [{ x, y, z, confidence, name }, ...],
      keypoints3D: [{ x, y, z, confidence, name }, ...],
      nose: { x, y, confidence, keypoint3D: { x, y, z, confidence } },
      left_eye_inner: { x, y, confidence, keypoint3D: { x, y, z, confidence } },
      left_eye: { x, y, confidence, keypoint3D: { x, y, z, confidence } },
      ...
      confidence: 0.28,
    },
    ...
  ];
  ```

  <!--
  ?> The `keypoints3D` array and `keypoint3D` property contain the 3D coordinates of the keypoints. The x, y, and z represent absolute distance in meters in a 2 x 2 x 2 meter cubic space. The range for each axis goes from -1 to 1 (therefore 2m total delta). The z is always perpendicular to the xy plane that passes the center of the hip, so the coordinate for the hip center is (0, 0, 0).
  -->
  ?> keypoints3D配列およびkeypoint3Dプロパティは、キーポイントの3D座標を含みます。x、y、zは、それぞれ2 x 2 x 2メートルの立方体空間における絶対距離をメートル単位で表しています。これらの値は、この立方体空間の中で定義されており、身体のキーポイントがこの空間内に収まるようになっています。各軸の範囲は-1から1まで（したがって、合計で2メートルの変化）です。z軸は常に、腰の中心を通るxy平面に対して垂直ですので、股関節の中心の座標は(0, 0, 0)になります。
  

---

### bodypose.detectStop()

<!--
This method can be called to stop the continuous pose estimation process.
-->
このメソッドは、動作し続けるポーズ推定のプロセスを停止するときに呼ぶことができます。

```javascript
bodypose.detectStop();
```

<!--
For example, you can toggle the pose estimation with click event in p5.js by using this function as follows:
-->
例えば、以下のようにこの関数を定義し、p5.jsのクリックイベントでポーズ推定を切り替えることができます：

```javascript
// Toggle detection when mouse is pressed
function mousePressed() {
  toggleDetection();
}

// Call this function to start and stop detection
function toggleDetection() {
  if (isDetecting) {
    bodypose.detectStop();
    isDetecting = false;
  } else {
    bodyPose.detectStart(video, gotPoses);
    isDetecting = true;
  }
}
```

---

### bodypose.detect()

<!--
This method runs the pose estimation on an image once, not continuously!
-->
このメソッドは連続的にではなく、一枚の画像に対して一度だけポーズ推定を行います！

```javascript
bodypose.detect(media, ?callback);
```

<!--
**Parameters:**
-->
**パラメータ:**

<!--
- **media**: An HTML or p5.js image, video, or canvas element to run the estimation on.

- **callback(results, error)**: Optional. A callback function to handle the results of the pose estimation. See the results above for an example of the model's output.
-->
- **media**: 推定を実行するHTMLまたはp5.js、画像、映像、またはキャンバス要素。

- **callback(results, error)**: オプション. ポーズ推定の結果を処理するコールバック関数。モデルの出力例については上記の結果を参照してください。

**Returns:**
**返り値:**

- **Array**: poses配列.

---

### bodypose.getConnections() / bodypose.getSkeleton()

<!--
This method returns an array of arrays, where each sub-array contains the indices of the connected keypoints.
-->
このメソッドは、２次元配列を返し、その中の各サブ配列は、接続されたキーポイントのインデックスを含みます。

```javascript
const connections;
function setup() {
  ...
  const connections = bodypose.getConnections(); // or bodypose.getSkeleton();
  ...
}
```

<!--
**Returns:**
-->
**返り値:**

<<<<<<< HEAD
<!--
- **Array**: An array of arrays representing the connections between keypoints. For example, using BlazePose model will returns:
-->
- **Array**: キーポイント間の接続を表す二次元配列。例えば、BlazePoseモデルを使用すると次のように返します:

=======
- **Array**: An array of arrays representing the connections between keypoints. For example, using BlazePose model will return:
>>>>>>> upstream/main

  ```js
  [[0, 1], [0, 4], [1, 2], ...[28, 32], [29, 31], [30, 32]];
  ```

<<<<<<< HEAD
<!--
This array represents the connections between keypoints, please refer to these images to understand the connections:
-->
この配列はキーポイント間の接続を表しています。キーポイントの接続を理解するのに、以下の画像を参照してください。
=======
  using MoveNet model will return:

  ```js
  [[0, 1], [0, 2], [1, 3], ...[12, 14], [13, 15], [14, 16]];
  ```

These arrays represents the connections between keypoints, please refer to these images to understand the connections:
>>>>>>> upstream/main

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
  <div style="text-align: center;">
    <h3>MoveNet</h3>
    <img style="display: block; max-width: 100%; margin: 0 auto;" alt="MoveNet keypoint diagram" src="./assets/BodyPose-MoveNet-Keypoints.png">
  </div>
  <div style="text-align: center;">
    <h3>BlazePose</h3>
    <img style="display: block; max-width: 100%; margin: 0 auto;" alt="BlazePose keypoint diagram" src="./assets/BodyPose-BlazePose-Keypoints.png">
  </div>
</div>
