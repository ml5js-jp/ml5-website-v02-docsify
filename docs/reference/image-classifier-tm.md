# Image + Teachable Machine

<center>
  <img class="header-img" src="assets/header-image-tm.png" alt="Image + Teachable Machine Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/admin885/" target="_blank" title="Juicy Fish">Juicy Fish</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

## Description

<!--
The ml5.js Image + Teachable Machine model allows you to create a model that can recognize the content of an image from a set of labels that you define. For example, you can train a model to tell the difference between a cat and a dog, happy and sad faces, or even between a hot dog and a sandwich.
-->

ml5.js Image + Teachable Machine を使うことによって、独自のラベルを用いて画像認識が行えるモデルを作成できます。例えば、犬と猫や幸せな顔と悲しい顔、あるいはホットドッグとサンドウィッチの違いが分かるモデルなども作ることができます。

<!--
The ml5.js Image + Teachable Machine model is a combination of [the ml5.js imageClassifier](/reference/image-classifier) and the Teachable Machine platform. Instead of using pre-trained models like MobileNet or Darknet, you can train your own model with the [Teachable Machine](https://teachablemachine.withgoogle.com/).
-->

ml5.js Image + Teachable Machineモデルというのはml5.js の画像分類機とTeachable Machineプラットフォームの組み合わせです。 MobileNetやDarknetのような学習済みモデルを使う代わりに、Teachable Machineを使って自分だけのモデルを学習させることができます。

<!--
?> If you are not familiar with the concept of image classification, we recommend checking out the [Image Classifier](/reference/image-classifier) guide first.
-->

?> もしあなたが画像分類についてわからなければ、先にImage Classifierのガイドをチェックするのがおすすめです。

<!--
It provides the following functionalities:
-->

ml5.js Image + Teachable Machineモデルによって、以下のことができるようになります。

<!--
- **Custom Labels**: Train your model with customized labels to recognize specific objects, animals, or people.
- **Image Classification**: The Image + Teachable Machine model can recognize the content of an image from a set of labels that you define.
- **Video Object Detection**: The Image + Teachable Machine model can also be used to classify objects into categories that you define in real-time video.
-->

  **独自のラベル**: 特定の物、動物、人を認識するために、独自のラベルを用いてモデルの学習を行えます。
　**画像の分類**: 独自のラベルを使って画像認識が行えます。
　**動画の物体検出**: リアルタイム映像の中で、物体を独自のカテゴリーごとに分類できます。

<!--
## Quick Start
-->

## クイックスタート


<!--
Run and explore a pre-built example! [This Image + Teachable Machine example](https://editor.p5js.org/ima_ml/sketches/vOSSEZwGf) classifies the content of an image from the webcam feed using a Teachable Machine model.
-->

築済みの例を動かして体験しましょう！ ml5.js Image +Teachable Machineモデルのサンプル ではTeachable Machineモデルを使用して、ウェブカメラから入力される画像の内容を分類します。

</br>

[DEMO](iframes/image-classifier-tm ":include :type=iframe width=100% height=550px")

<!--
## Examples
-->

## 例

<!--
- [Image + Teachable Machine Video](https://editor.p5js.org/ima_ml/sketches/vOSSEZwGf): Classify the content of an image from the webcam feed using a Teachable Machine model.
-->

- [Image + Teachable Machine Video](https://editor.p5js.org/ima_ml/sketches/vOSSEZwGf):  Teachable Machineモデルを使ってウェブカメラから入力される画像の内容を分類しましょう。

<!--
## Step-by-Step Guide
-->

## ステップバイステップガイド

<!--
Now, let's together build the [Image + Teachable Machine Video example](https://editor.p5js.org/ima_ml/sketches/vOSSEZwGf) from scratch, and in the process, learn how to use the Image + Teachable Machine model.
-->

ゼロから一緒にml5.js+Teachable Machine ビデオのサンプルをビルドして、ml5.js+Teachable Machineモデル の使い方を学びましょう。

<!--
### Create a new project
-->

### 新規プロジェクトを作成する

<!--
To follow along, start by creating an empty project in the [p5.js web editor](https://editor.p5js.org/).
-->

P5.js web editorで新規プロジェクトを作成することから始めましょう。

<!--
### Set up ml5.js
-->

### Ml5.jsのセットアップする

<!--
Import the ml5.js library in your `index.html` file.
-->

Ml5.jsライブラリをindex.htmlファイルにインポートします。

```html
<script src="https://unpkg.com/ml5@1/dist/ml5.js"></script>
```

<!--
?> If you are not familiar with how to import the ml5.js library and need more detailed guidance, please check out our [Getting Started](/?id=set-up-ml5js) page.
-->

もし、ml5.jsライブラリのインポートの仕方が分からなかったり、より詳しい説明が必要な場合はGetting Started を確認してください。

<!--
### Load model
-->

### モデルを読み込む

<!--
Let's open the `sketch.js` file and define a variable to store the Image + Teachable Machine model.
-->

sketch.jsを開いてml5.js＋Teachable Machine modelを扱う変数を定義しましょう。

```javascript
let classifier;
```

<!--
Before we load the model, we need to get the model URL from the Teachable Machine platform. Follow the steps below to create a Teachable Machine model:
-->

モデルを読み込む前に、Teachable Machine プラットフォームからモデルのURLを取得しておきましょう。Teachable Machineモデルを作成するには下記のステップに従ってください。

<!--
- Step 1: Open [Teachable Machine](https://teachablemachine.withgoogle.com/train) and create a new "Image Project".
- Step 2: Choose "Standard image model".
- Step 3: Click the "Edit" icon to rename "Class 1" to your desired label. In our case, "thermos".
- Step 4: Click the "Webcam" icon and long press "Hold to Record" button to capture some thermos photos.
- Step 5: Repeat steps 3 and 4 for the second labels, in our case "eraser". If you need more than two labels, click "Add a class", and then rename "Class 3" (or 'Class 4,' 'Class 5,' etc.) to whatever you prefer.
- Step 6: Click the "Train Model" button to train your model.
- Step 7: Click the "Export Model" button, and in the pop-up window, click the "Upload my model" button to get the model URL.
- Step 8: Copy the model URL in the "Your shareable link" field.
-->

-	ステップ1：Teachable Machineを開き、新規”Image Project“を作成
-	ステップ2:”Standard image model”を選択
-	ステップ３:”Edit”アイコンをクリックして”Class 1”を望むラベルの名前に変更する。サンプルは”daytime”
-	ステップ4:”Webcam”アイコンをクリックする。”Hold to Record”ボタンを長押しして何枚かの幸せな顔画像のサンプルを取得
-	ステップ5:ステップ3と4を繰り返して二つ目のラベルを作る。サンプルは”nighttime”。もしもっとラベルが必要なら、”Add a class”をクリックして現れたClass3(あるいはClass4、Class5)を望む名前に変更する。
-	ステップ6:”Train Model”ボタンをクリックしモデルの学習を行う。
-	ステップ7：”Export Model”ボタンをクリック、pop-up window内の”Upload my model”ボタンをクリックしモデルのURLを取得する。
-	ステップ8：モデルのURLを”Your shareable link”の領域にコピーする。

<!--
After we have the model URL, we can store it in a variable in the `sketch.js` file.
-->

モデルのURLを取得した後、それをsketch.jsファイル内の変数に保存します。

```javascript
let imageModelURL = "https://teachablemachine.withgoogle.com/models/4-WUyljZZ/";
```

<!--
Now, we can load the model that we just trained in the `preload` function. Using the `preload` function ensures that the model is loaded before the `setup` and `draw` functions are called.
-->
これで、preload関数で学習モデルを読み込むことができます。preload関数を使うことでセットアップ前のモデルの読み込みとdrow関数の呼び出しがおこなわれます。

```javascript
function preload() {
  classifier = ml5.imageClassifier(imageModelURL + "model.json", {
    flipped: true,
  });
}
```
<!--
### Fetch webcam video
-->

### ウェブカメラからの動画取得

<!--
Define a variable `video` to hold the webcam video.
-->

ウェブカメラのビデオを保持するための変数videoを定義します。

```javascript
let video;
```
<!--
Resize the canvas dimensions to 640x480, a common resolution for webcams.
-->

ウェブカメラに共通の解像度である640x480にサイズを変更します。

```javascript
function setup() {
  createCanvas(640, 480);
}
```
<!--
Fetch the webcam video, resize it to fit the canvas, and hide it from the display.
-->

ウェブカメラのビデオを取得し、キャンバスに合うようにサイズを変更します。そして画面から動画を隠します。

```javascript
  // Create the video and hide it
  video = createCapture(VIDEO, { flipped: true });
  video.size(320, 240);
  video.hide();
}
```

<!--
### Classify the video with the model
-->

### モデルを用いた動画を分類する

<!--
To store the classification result, define a variable `label`.
-->

分類結果を保存するために、変数labelを定義します。

```javascript
let label = "";
```

<!--
We can now start classifying the video with the Teachable Machine model. In the `setup` function, call the `classifyStart` method on the `classifier` object.
-->

これでTeachable Machine modelを用いて動画の分類を始めることができます。Setup functionで、classifier オブジェクトのclassifyStartメソッドを呼び出します。

```javascript
function setup() {
  ...
  video.hide();

  // Start classifying the video
  classifier.classifyStart(video, gotResult);
}
```

<!--
The `gotResult` function is a callback function that will be called when the `classifyStart` method finishes classifying the video. Now, let's define the `gotResult` function. This function will update the `label` variable with the highest confidence label predicted by the model.
-->

gotResult 関数はclassifyStartメソッドが動画の分類を終えた時に呼ばれるコールバック関数です。この関数はモデルが予測した中で最も信頼度の高いラベルを用いてlabelの変数を上書きします。

```javascript
// A function to run when we get the results and any errors
function gotResult(results) {
  // Update the label variable which is displayed on the canvas
  label = results[0].label;
}
```

<!--
### Display the results
-->

### 結果を表示する

<!--
Before we display the label predicted by the model, we need to draw the webcam video on the canvas.
-->

モデルによって予測されたラベルを表示する前に、ウェブカメラの動画をキャンバスに映しましょう。

```javascript
function draw() {
  image(video, 0, 0, width, height);
}
```

<!--
Now, we can display the classification result on the canvas.
-->

その後、キャンバスに分類の結果を表示します。

```javascript
  // Display the label on the canvas
  fill(255);
  textSize(16);
  textAlign(CENTER);
  text(label, width / 2, height - 4);
}
```

<!--
### Run your sketch
-->

### Sketchを実行する

<!--
Congratulations! You have successfully built the Image + Teachable Machine Video example. Press the <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `run` button to see the code in action. You can also find the [complete code](https://editor.p5js.org/ima_ml/sketches/vOSSEZwGf) in the p5.js web editor.
-->

Congratulations! You have successfully built the Image + Teachable Machine Video example. Press the run button to see the code in action. You can also find the complete code in the p5.js web editor.

<!--
?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better.
-->

?> もしステップバイステップのコードガイドの中で何か疑問や明確でない部分があればお聞かせください。Discordに参加して、どのように改善できるかおしえてください。

<!--
## Properties
-->

## プロパティ

### imageClassifier.modelName

<!--
- **Description**
  - The name of the model being used, typically one of "mobilenet", "darknet", "darknet-tiny", or "doodlenet".
- **Type**
  - String
-->

- **説明**
  - 使われるモデルの名前。mobilenet、darknet、darknet-tinyやdoodlenet等が典型的に使われている
- **型**
  - String

---

### imageClassifier.modelUrl

<!--
- **Description**
  - The URL of the model if a custom model is being used.
- **Type**
  - String
-->

- **説明**
  - カスタムモデルを使用している場合は、モデルのURL
- **型**
  - string

---

### imageClassifier.model

<!--
- **Description**
  - The TensorFlow.js model used for image classification.
- **Type**
  - tf.LayersModel
-->

- **説明**
  - 画像分類に使われているTensorFlow.jsモデル
- **型**
  - tf.LayersModel

---

### imageClassifier.modelToUse

<!--
- **Description**
  - The specific model module to be used for image classification, such as MobileNet, Darknet, or Doodlenet.
- **Type**
  - Object
-->

- **説明**
  - MobileNet、DarknetやDoodlenetのような画像分類に用いられている特定のモデルのモジュール
- **型**
  - Object
---

### imageClassifier.mapStringToIndex

<!--
- **Description**
  - An array mapping string labels to indices for custom models.
- **Type**
  - Array
-->

- **説明**
  - 文字列のラベルをカスタムモデルのインデックスに対応させる配列
- **型**
  - Array

---

### imageClassifier.version

<!--
- **Description**
  - The version of the model being used, applicable to MobileNet.
- **Type**
  - Number
-->

- **説明**
  - 使用されているモデルのバージョン。MobileNetに適応されている
- **型**
  - Number

---

### imageClassifier.alpha

<!--
- **Description**
  - The alpha value (width multiplier) of the model being used, applicable to MobileNet.
- **Type**
  - Number
-->

- **説明**
  - 使用されているモデルのアルファ値(width multiplier)。MobileNetに適応されている
- **型**
  - Number

---

### imageClassifier.topk

<!--
- **Description**
  - The number of top predictions to return, applicable to MobileNet.
- **Type**
  - Number
-->

- **説明**
  - o	戻り値の中で最も高い予測の数値。MobileNetに適応されている
- **型**
  - Boolean

---

### imageClassifier.isClassifying

<!--
- **Description**
  - A flag indicating whether the classification loop is currently running.
- **Type**
  - Boolean
-->

- **説明**
  - 分類のためのループがその時も動いているか示すフラグ
- **型**
  - Boolean

---

### imageClassifier.signalStop

<!--
- **Description**
  - A flag used to signal the classification loop to stop.
- **Type**
  - Boolean
-->

- **説明**
  - 分類のループが停止していることを伝えるために使われるフラグ
- **型**
  - Boolean

---

### imageClassifier.prevCall

<!--
- **Description**
  - Tracks the previous call to `classifyStart` or `classifyStop` to handle warnings.
- **Type**
  - String
-->

- **説明**
  - Warning制御をするための過去のclassifyStartやClassifyStopの呼び出しの追跡
- **型**
  - String

---

### imageClassifier.ready

<!--
- **Description**
  - A promise that resolves when the model has loaded.
- **Type**
  - Promise
-->

- **説明**
  - モデルの読み込みの完了により解決するPromise処理
- **型**
  - Promise

## Methods

#### ml5.imageClassifier()

<!--
This method is used to initialize the imageClassifer object. Here, you could provide the teachable machine model URL to load the model.
-->

このメソッドはimageClassifierオブジェクトの初期化に使われます。これにはモデルを読み込むためのteachable machine モデルのURLを渡すことができます。

```javascript
const classifier = ml5.imageClassifier(imageModelURL + "model.json");
```

<!--
**Returns:**
-->

**戻り値**  
The imageClassifier object.

---

#### imageClassifier.classifyStart()

<!--
This method repeatedly outputs classification labels on an image media through a callback function.
-->

このメソッドはコールバック関数を通して画像媒体の分類ラベルを繰り返し出力します。

```javascript
imageClassifier.classifyStart(media, ?kNumber, callback);
```

<!--
**Parameters:**

- **media**: An HTML or p5.js image, video, or canvas element to run the classification on.
- **kNumber**: The number of labels returned by the image classification.
- **callback(output, error)**: A callback function to handle the output of the classification. See below for an example output passed into the callback function:
-->

**パラメータ**
- **media**: 分類を実行するためのHTMLかp5.jsの画像、動画、あるいはキャンバスの要素
- **kNumber**: 画像分類が返したラベルの数
- **callback(output, error)**: 分類の出力を制御するためのコールバック関数。以下が、コールバック関数が呼び出される出力の例である:


  ```javascript
  [
    {
      label: "cat",
      confidence: 0.99,
    },
    {
      label: "dog",
      confidence: 0.01,
    },
  ];
  ```

---

#### imageClassifier.classifyStop()

<!--
This method can be called after a call to `imageClassifier.classifyStart` to stop the repeating classifications.
-->

このメソッドは分類の繰り返しを止めるためにimageClassifier.classifyStartが呼び出された後に呼び出されます。

```javascript
imageClassifier.classifyStop();
```

---

#### imageClassifier.classify()

<!--
This method asynchronously outputs a single image classification on an image media when called.
-->

このメソッドは呼び出されたとき画像媒体の一つの画像の分類を非同期に出力します。

```javascript
imageClassifier.classify(media, ?kNumber, ?callback);
```

<!--
**Parameters:**

- **media**: An HTML or p5.js image, video, or canvas element to run the classification on.
- **kNumber**: The number of labels returned by the image classification.
- **callback(output, error)**: Optional. A callback function to handle the output of the classification.

**Returns:**  
A promise that resolves to the estimation output.
-->

**パラメータ**
- **media**: 分類を実行するためのHTMLかp5.jsの画像、動画、あるいはキャンバスの要素
- **kNumber**: 画像分類から戻ったラベルの数
- **callback(output, error)**: option. 分類の出力を制御するためのコールバック関数

**戻り値**
推定の出力があった時解決するpromise処理
