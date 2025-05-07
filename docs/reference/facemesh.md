# FaceMesh

<center>
  <img class="header-img" src="assets/header-facemesh.png" alt="FaceMesh Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/pglen/" target="_blank" title="Paweł Gleń">Paweł Gleń</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

## 概要

<!-- 
FaceMesh is a machine-learning model that allows for facial landmark detection in the browser. It can detect multiple faces at once and provides 468 3D facial landmarks that describe the geometry of each face. FaceMesh works best when the faces in view take up a large percentage of the image or video frame and it may struggle with small/distant faces.
 -->
FaceMesh は、ブラウザ内で顔のキーポイントを検出するための機械学習モデルです。複数の顔を同時に検出することができ、それぞれの形状を説明する468個の3Dランドマークを提供します。FaceMesh は、画像やビデオフレーム内で顔が大部分を占める場合に最もよく動作し、顔が小さかったり遠かったりするとうまく動かないことがあります。 

<!-- 
The ml5.js FaceMesh model is ported from the [TensorFlow.js FaceMesh implementation](https://github.com/tensorflow/tfjs-models/tree/master/face-landmarks-detection). 
-->
ml5.js の FaceMesh モデルは、[TensorFlow.js の FaceMesh](https://github.com/tensorflow/tfjs-models/tree/master/face-landmarks-detection) 実装から移植されています。

<!-- 
t provides the following functionalities:
 -->
このモデルは、以下の機能を提供します：

<!-- 
- **Facial Landmark Detection**: Detect the 3D coordinates of 468 keypoints on the face.
- **Face Bounding Box**: Provide the bounding box of each detected face.
- **Multiple Faces**: Detect multiple faces at the same time. You can specify the maximum number of faces to detect.
-->
- **顔のランドマーク検出**: 468個の顔のキーポイントの3D座標を検出する。
- **顔のバウンディングボックス**: 検出された顔の領域を囲う枠 を提供する。 
- **複数の顔**: 複数の顔を同時に検出できます。検出する顔の最大数を指定することができる。

<!--
## Quick Start
-->
## クイックスタート!


<!-- 
Run and explore a pre-built example! [This FaceMesh example](https://editor.p5js.org/ml5/sketches/lCurUW1TT) displays 468 facial landmarks that describe the geometry of each face in real-time from the webcam. 
-->
事前に構築されたサンプルを実行して見てみましょう！ [このFaceMesh のサンプル](https://editor.p5js.org/ml5/sketches/lCurUW1TT)は、Webカメラからリアルタイムで各顔の形状を説明する468個の顔ランドマークを表示します。
</br>

[DEMO](iframes/facemesh ":include :type=iframe width=100% height=550px")

<!--
## Examples
-->
## サンプル


<!-- 
- [FaceMesh Keypoints](https://editor.p5js.org/ml5/sketches/lCurUW1TT): Draw the keypoints of the detected face from the webcam.
- [FaceMesh Single Image](https://editor.p5js.org/ml5/sketches/lqQZrDJHF): Detect the keypoints of the face from a single image.
- [FaceMesh Parts](https://editor.p5js.org/ml5/sketches/9y9W7eAee): Draw specific face parts of the detected face. -->
- [FaceMesh キーポイント](https://editor.p5js.org/ml5/sketches/lCurUW1TT): Webカメラから検出された顔のキーポイントを描きます。
- [FaceMesh 単一画像](https://editor.p5js.org/ml5/sketches/lqQZrDJHF): 1枚の画像から顔のキーポイントを検出します。
- [FaceMesh パーツ](https://editor.p5js.org/ml5/sketches/9y9W7eAee): 検出された顔の特定の部分を描きます。



<!--
## Step-by-Step Guide
-->
## 段階的なガイド

<!-- 
Now, let's together build the [FaceMesh Keypoints example](https://editor.p5js.org/ml5/sketches/lCurUW1TT) from scratch, and in the process, learn how to use the FaceMesh model. 
-->
それでは一緒にFaceMesh Keypoints exampleをゼロから構築しましょう！その過程で、FaceMeshモデルの使い方を学ぶことができます！


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
Import the ml5.js library in your `index.html` file. 
-->
index.html ファイルに ml5.js ライブラリをインポートします。

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
Let's open the `sketch.js` file and define a variable to store the FaceMesh model. 
-->
sketch.js ファイルを開いて、FaceMesh モデルを保存する変数を定義しましょう。

```javascript
let faceMesh;
```

<!-- 
Next, we can create a `options` object to customize the model's behavior. For example, we can set the maximum number of faces to detect to 1, disable the refinement of landmarks (further refine the landmark coordinates around the eyes and lips at the cost of compute), and prevent the model from flipping the image horizontally. 
-->
次に、モデルの動作をカスタマイズするための`options`オブジェクトを作成できます。例えば、検出する顔の最大数を1に設定し、ランドマークの精度を高めるオプションを無効にし（目と唇周辺の座標を細かく得ることができますが 、計算量が増えます）、画像が水平に反転しないように設定できます。

```javascript
let options = { maxFaces: 1, refineLandmarks: false, flipped: false };
```

<!-- 
?> If you would like to know more about the available configuration settings for `options`, please check out the [Methods](/reference/facemesh?id=methods) section. 
-->
?> もし `options`に関する設定についてもっと知りたい場合は、[Methods](/reference/facemesh?id=methods) セクション をチェックしてください

<!-- 
Now, we are ready to load a model configed as `options` specifies and store it in the `faceMesh` variable. 
-->
さて、`options`で指定した設定でモデルを読み込み、それを `faceMesh` 変数に保存する準備が整いました。

<!-- 
Let's create a `preload` function to load the FaceMesh model. The `preload` function is a p5.js function that runs before the `setup` and `draw` function. This is where we load the model to ensure it is ready before we use it. 
-->
FaceMeshモデルを読み込むために、`preload`関数を作成しましょう。`preload` 関数は、`setup` と `draw` 関数の前に実行される p5.js の関数です。ここでモデルを読み込むことで、使用する前に準備が整っていることを確認します。

```javascript
function preload() {
  faceMesh = ml5.faceMesh(options);
}
```

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
### Detect keypoints with the model 
-->
### モデルでキーポイントを検出する

<!-- 
Define a `faces` variable to store the detected faces. Note that the `faces` variable will store an array of detected faces, and each face has a property `keypoints` that will contain an array of keypoints. 
-->
検出された顔を保存するために  変数`faces`を定義します。この 変数`faces` は検出された顔の配列を保存します。各facesオブジェクトには `keypoints` というプロパティがあり、その中にキーポイントの配列が含まれます。

```javascript
let faces = [];
```

<!-- 
To start detecting the keypoints of the face, in the `setup` function, we need to call the `detectStart` method of the `faceMesh` object. This method takes the webcam video as input and a callback function to handle the output. 
-->
顔のキーポイントの検出を開始するには、`setup` 関数内で `faceMesh` オブジェクトの `detectStart` メソッドを呼び出す必要があります。このメソッドは、Webカメラのビデオを引数として受け取り、出力を処理するためのコールバック関数を使用します。

```javascript
function setup() {
  ...
  video.hide();

  // Start detecting faces from the webcam video
  faceMesh.detectStart(video, gotFaces);
}
```

<!-- 
The `gotFaces()` function is a callback function that will be called when the `faceMesh.detectStart()` method detects faces. Once the faces are detected, the output `results` will be passed to `gotFaces()`, and then saved to the `faces` variable. 
-->
`gotFaces()`関数は、`faceMesh.detectStart()`メソッドが顔を検出した時に呼び出されるコールバック関数です。顔が検出されると、出力の`results`は`gotFaces()`に渡され、そして変数`faces`に保存されます。



```javascript
// Callback function for when faceMesh outputs data
function gotFaces(results) {
  // Save the output to the faces variable
  faces = results;
}
```

<!-- 
### Draw keypoints on the canvas 
-->
### キャンバスにキーポイントを描画する

<!-- 
In the `draw()` function, draw the webcam video on the canvas. 
-->
`draw()` 関数内で、ウェブカメラの映像をキャンバスに描画します。 

```javascript
function draw() {
  image(video, 0, 0, width, height);
```

<!-- 
Iterate all faces of the `faces` array, fetch the `i`th dectected face, and store it in the `face` variable. 
-->
配列`faces`を反復処理し、検出された `i`番目の顔を取得し、それを変数`face`に保存します。 

```javascript
// Draw all the tracked face points
  for (let i = 0; i < faces.length; i++) {
    let face = faces[i];
```

<!-- 
Iterate though all the keypoints of the `i`th detected face, fetch the `j`th keypoint, and store it in the `keypoint` variable. 
-->
検出された`i`番目のfaceのキーポイント配列を反復処理し、`j`番目のキーポイントを取得し、それを変数`keypoint`に保存します。 

```javascript
    for (let j = 0; j < face.keypoints.length; j++) {
      let keypoint = face.keypoints[j];
```

<!-- 
Draw a green circle at the location of the `j`th keypoint. 
-->
`j`番目のキーポイントの位置に緑色の円を描画します。 

```javascript
      fill(0, 255, 0);
      noStroke();
      circle(keypoint.x, keypoint.y, 5);
    }
  }
}
```

<!-- 
Note we are iterating through all the keypoints (`j` is ranging from 0 to the length of the keypoints array) of the detected face (`i` is ranging from 0 to the length of the faces array). This will result in green landmarks on all detected face(s) in the webcam video. In our case, we set the maximum number of faces to detect to 1 in the `options` object (`maxFaces: 1`), so we will only see landmarks on one face. 
-->
注意：ここでは、すべての検出された顔の keypoints 配列のすべてのキーポイントを反復処理しています (`j`は keypoints 配列の長さまで、`i`は faces 配列の長さまで範囲があります)。これにより、ウェブカメラ映像内のすべての検出された顔に緑色のキーポイントが表示されます。今回の場合、`options` オブジェクトで検出する顔の最大数を1に設定しているため (`maxFaces: 1`)、ランドマークは1つの顔にのみ表示されます。 

<!--
### Run your sketch
-->
### スケッチを実行する

<!-- 
And, that's it! You have successfully built the FaceMesh Keypoints example from scratch. Press the <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="tip icon" aria-hidden="true"> `run` button to see the code in action. You can also find the complete code [here](https://editor.p5js.org/ml5/sketches/lCurUW1TT). 
-->
これで完成です！ゼロから FaceMesh キーポイントサンプルを無事に構築できました。`実行`<img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="tip icon" aria-hidden="true">ボタンを押して、コードがどのように動作するかを確認しましょう。また、完全なコードは こちら[here](https://editor.p5js.org/ml5/sketches/lCurUW1TT)からも確認できます。 


<!--
?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better.
-->
?> この段階的なコードガイドで質問や不明点がございましたら、ぜひご連絡ください。[Discord](https://discord.com/invite/3CVauZMSt7)に参加して、改善点をお知らせください。

<!--
## Properties
-->
## プロパティ

### faceMesh.model

<!-- 
- **Description**
  - The TensorFlow.js model used for face landmarks detection.
- **Type**
  - tf.LayersModel 
  -->
- **説明**
  - 顔のランドマーク検出に使用される TensorFlow.js モデル。
- **型**
  - tf.LayersModel

---

### faceMesh.config

<!-- 
- **Description**
  - Configuration options provided by the user for the model.
- **Type**
  - Object 
  -->
- **説明**
  - ユーザーがモデルに提供する設定オプション。
- **型**
  - Object
---

### faceMesh.runtimeConfig

<!-- 
- **Description**
  - Configuration options related to the runtime behavior of the model.
- **Type**
  - Object 
  -->
- **説明**
  - モデルの動作に関する設定オプション。
- **型**
  - Object  

---

### faceMesh.detectMedia

<!-- 
- **Description**
  - The media element (image, video, or canvas) on which face detection is performed.
- **Type**
  - HTMLElement 
  -->
- **説明**
  - 顔検出を行うメディア要素（画像、ビデオ、またはキャンバス）。
- **型**
  - HTMLElement  
---

### faceMesh.detectCallback

<!-- 
- **Description**
  - The callback function to handle face detection results.
- **Type**
  - Function 
  -->
- **説明**
  - 顔検出の結果を処理するコールバック関数。
- **型**
  - Function    

---

### faceMesh.detecting

<!-- 
- **Description**
  - A flag indicating whether the detection loop is currently running.
- **Type**
  - Boolean 
  -->
- **説明**
  - 現在、検出ループが実行中かどうかを示すフラグ。
- **型**
  - Boolean    

---

### faceMesh.signalStop

<!-- 
- **Description**
  - A flag used to signal the detection loop to stop.
- **Type**
  - Boolean 
  -->
- **説明**
  - 検出ループを停止するためのフラグ。
- **型**
  - Boolean    
---

### faceMesh.prevCall

<!-- 
- **Description**
  - Tracks the previous call to `detectStart` or `detectStop` to handle warnings.
- **Type**
  - String 
  -->
- **説明**
  - detectStart または detectStop の前回の呼び出しを記録し、警告を処理するために使用。
- **型**
  - String    

---

### faceMesh.ready

<!-- 
- **Description**
  - A promise that resolves when the model has loaded.
- **Type**
  - Promise 
  -->
- **説明**
  - モデルが読み込まれたときに解決される Promise。
- **型**
  - Promise  

<!-- 
## Methods 
-->
## メソッド

### ml5.faceMesh()

<!-- 
This method is used to initialize the faceMesh object. 
-->
このメソッドは、FaceMesh オブジェクトを初期化するために使用されます。 

```javascript
const faceMesh = ml5.faceMesh(?options, ?callback);
```

**Parameters:**

<!-- 
- **options**: Optional. An object to change the default configuration of the model. The default and available options are: 
-->
**options**:オプション。モデルのデフォルト設定を変更するためのオブジェクトです。デフォルトの設定および利用可能なオプションは：

  ```javascript
  {
      maxFaces: 1,
      refineLandmarks: false,
      flipped: false
  }
  ```

  <!-- 
  Options for face detection: 
  -->
  顔検出のためのオプション:

  <!-- 
  - _maxFacess_
    - Number: The maximum number of faces to detect. Defaults to 2.
  - _refineLandmarks_
    - Boolean: Refine the landmarks. Defaults to false.
  - _flipped_
    - Boolean: Flip the result horizontally. Defaults to false.
  - _runtime_
    - String: The runtime to use. "tfjs" (default) or "mediapipe". 
    -->
  - _maxFacess_
    - Number: 検出する顔の最大数。デフォルトは2です。
  - _refineLandmarks_
    - Boolean: ランドマークをより精密に表示するかどうか。デフォルトは false です。
  - _flipped_
    - Boolean: 結果を水平に反転するかどうか。デフォルトは false です。
  - _runtime_
    - String: 使用するランタイムを指定します。デフォルトは "tfjs"、または "mediapipe" が選択可能です。

  <!-- 
  For using custom or offline models: 
  -->
  カスタムモデルまたはオフラインモデルを使用する場合

  <!-- 
  - _solutionPath_
    - String: The file path or URL to the model. 
    -->
  - _solutionPath_
    - String: モデルのファイルパスまたはURLを指定します。

  <!-- 
  More info on options [here](https://github.com/tensorflow/tfjs-models/tree/master/face-landmarks-detection/src/mediapipe#create-a-detector). 
  -->
  詳しいオプションの情報は、[こちら](https://github.com/tensorflow/tfjs-models/tree/master/face-landmarks-detection/src/mediapipe#create-a-detector)をご覧ください。 

<!-- 
- **callback(faceMesh, error)**: Optional. A function to run once the model has been loaded. Alternatively, call `ml5.faceMesh()` within the p5 `preload` function. 
-->
- **callback(faceMesh, error)**: オプション。モデルの読み込みが完了した際に実行される関数。または、p5 の `preload` 関数内で `ml5.faceMesh()` を呼び出すことも可能です。 

 

<!-- 
**Returns:** 
-->
**返り値:**

<!-- 
- **Object**: The faceMesh object. This object contains the methods to start and stop the detection process. 
-->
- **Object**: FaceMesh オブジェクト。このオブジェクトには、検出プロセスを開始および停止するためのメソッドが含まれています。

---

### faceMesh.detectStart()

<!-- 
This method repeatedly outputs face estimations on an image media through a callback function. 
-->
このメソッドは、コールバック関数て、画像メディアの顔推定結果を繰り返し出力します。 

```javascript
faceMesh.detectStart(media, callback);
```

<!-- 
**Parameters:** 
-->
**パラメータ:**

<!-- 
- **media**: An HTML or p5.js image, video, or canvas element to run the estimation on.
- **callback(results, error)**: A callback function to handle the output of the estimation. See below for an example output passed into the callback function: 
-->
- **media**: 推定を実行するための要素。HTMLまたはp5.js画像、映像またはキャンバス。
- **callback(results, error)**: 推定の出力を処理するためのコールバック関数。以下は、コールバック関数に渡される出力例です： 

  ```javascript
  [
    {
      box: { width, height, xMax, xMin, yMax, yMin },
      keypoints: [{ x, y, z, name }, ... ],
      faceOval: { x, y, width, height, centerX, centerY, keypoints: [{ x, y, z }, ... ]},
      leftEye: { x, y, width, height, centerX, centerY, keypoints: [{ x, y, z }, ... ]},
      ...
    },
    ...
  ]
  ```

  <!-- 
  [Here](https://github.com/tensorflow/tfjs-models/blob/master/face-landmarks-detection/mesh_map.jpg) is a diagram for the position of each keypoint (download and zoom in to see the index). 
  -->
  [こちらは](https://github.com/tensorflow/tfjs-models/blob/master/face-landmarks-detection/mesh_map.jpg) 各キーポイントの位置を示した図です（ダウンロードして拡大するとインデックスが確認できます）。

---

### faceMesh.detectStop()

<!-- 
This method can be called after a call to `faceMesh.detectStart` to stop the repeating face estimation. 
-->
このメソッドは、`faceMesh.detectStart` を呼び出した後に、繰り返し行われる顔の推定を停止するために使用できます。  

```javascript
faceMesh.detectStop();
```

---

### faceMesh.detect()

<!-- 
This method asynchronously outputs a single face estimation on an image media when called. 
-->
このメソッドは、画像メディアから1回だけ顔を検出して結果を返します（非同期的に動作します）。 


```javascript
faceMesh.detect(media, ?callback);
```

<!--
**Parameters:**
-->
**パラメータ:**

<!-- 
- **media**: An HTML or p5.js image, video, or canvas element to run the estimation on.
- **callback(results, error)**: Optional. A callback function to handle the output of the estimation, see output example above. 
-->
- **media**: 推定を実行するHTMLまたはp5.js、画像、映像、またはキャンバス要素。
- **callback(results, error)**: オプション。推定結果を処理するためのコールバック関数です。出力例は上記を参照してください。
