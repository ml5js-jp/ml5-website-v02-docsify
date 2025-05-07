# ImageClassifier

<center>
  <img class="header-img" src="assets/header-image-classifier.png" alt="ImageClassifier Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/naveena.160" target="_blank" title="Naveen">Naveen</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

<!-- 
## Description 
-->
## 概要

<!-- 
The ml5.js imageClassifier is a pre-trained model that can recognize the content of an image. It can identify objects, animals, and even people in a picture. The image classifier uses a neural network to analyze the image and provide a list of possible labels for the content of the image in its entirety.

The ml5.js imageClassifier uses the pre-trained MobileNet model by default. You can optionally load and use other models such as Darknet as well as a custom-trained model, DoodleNet, which is also built upon the MobileNet architecture and trained on images from the Google _Quick, Draw!_ dataset. 
-->
ml5.js の imageClassifier は、画像の内容を認識できる事前に学習されたモデルです。画像内の物体、動物、さらには人物を識別することができます。この画像分類器はニューラルネットワークを使用して画像を分析し、画像全体の内容に基づいた可能性のあるラベルのリストを提供します。 

ml5.js の imageClassifier はデフォルトで事前に学習された MobileNet モデルを使用しますが、Darknet のような他のモデルや、Google Quick, Draw! データセットの画像で学習されたカスタムトレーニングモデル DoodleNet もオプションで読み込むことができます。 

<!-- 
It provides the following functionality: 
-->
以下の機能を提供します：

<!-- 
- **Image Classification**: ImageClassifier can recognize the content of an image and provide a list of possible labels.
- **Video Object Detection**: ImageClassifier can also be used to classify objects in a video stream. 
-->
- **画像分類**: imageClassifier は画像の内容を認識し、可能性のあるラベルのリストを提供します。
- **ビデオオブジェクト検出**: imageClassifier は、ビデオストリーム内のオブジェクト分類にも使用できます。 

<!-- 
?> If you want to **train your own image classification model with customized labels**, check out our [Image + Teachable Machine](/reference/image-classifier-tm) to get started! 
-->
?> **自分で独自のラベルを使った画像分類モデルをトレーニング**したい場合は、 [Image + Teachable Machine](/reference/image-classifier-tm) をチェックして、始めましょう！

<!--
## Quick Start
-->
## クイックスタート!


<!-- 
Run and explore a pre-built example! [This ImageClassifier example](https://editor.p5js.org/ml5/sketches/pjPr6XmPY) classifies the content of an image and displays the results on the canvas. 
-->
事前に構築されたサンプルを実行して見てみましょう！[この ImageClassifier サンプル](https://editor.p5js.org/ml5/sketches/pjPr6XmPY) は、画像の内容を分類し、結果をキャンバスに表示します。 

</br>

[DEMO](iframes/image-classifier ":include :type=iframe width=100% height=550px")

<!--
## Examples
-->
## サンプル

<!-- 
- [ImageClassifier Single Image](https://editor.p5js.org/ml5/sketches/pjPr6XmPY): Classify the content of an image and display the results on the canvas.
- [ImageClassifier Video](https://editor.p5js.org/ml5/sketches/K0sjaEO19): Classify the content of objects in a video stream. 
-->
- [ImageClassifier Single Image](https://editor.p5js.org/ml5/sketches/pjPr6XmPY): 画像の内容を分類し、結果をキャンバスに表示します。
- [ImageClassifier Video](https://editor.p5js.org/ml5/sketches/K0sjaEO19): ビデオストリーム内のオブジェクトの内容を分類します。 

<!--
## Step-by-Step Guide
-->
## 段階的なガイド

<!--
Now, let's together build the [ImageClassifier Single Image example](https://editor.p5js.org/ml5/sketches/pjPr6XmPY) from scratch, and in the process, learn how to use the ImageClassifier model. 
-->
それでは一緒に[ImageClassifier Single Image example](https://editor.p5js.org/ml5/sketches/pjPr6XmPY) をゼロから構築しましょう！その過程で、ImageClassifierモデルの使い方を学ぶことができます！


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

<!-- Let's open the `sketch.js` file and define a variable to store the ImageClassifier model. -->
sketch.js ファイルを開いて、ImageClassifier モデルを保存するための変数を定義しましょう。 

```javascript
let classifier;
```

<!-- 
Now, we can load the ImageClassifier model in the `preload` function. Using the `preload` function ensures that the model is loaded before the `setup` and `draw` functions are called. Note here we can specify the model name we want to use, such as `MobileNet`. 
-->
`preload` 関数で ImageClassifier モデルを読み込みます。`preload` 関数を使うことで、`setup` 関数や `draw` 関数が呼び出される前にモデルが読み込まれていることを保証します。ここでは、使用するモデル名（例えば `MobileNet`）を指定できます。 

```javascript
function preload() {
  classifier = ml5.imageClassifier("MobileNet");
}
```

<!-- 
?> If you would like to use a different model such as `Darknet`, specify configuration options for the model, or tailor a callback function to run once the model is loaded, you can pass these as arguments to the `ml5.imageClassifier(?modelName, ?options, ?callback)` method. See the [ml5.imageClassifier() method](/reference/image-classifier?id=ml5imageclassifier) for more details. 
-->
?> もし、Darknet などの別のモデルを使用したい場合、またはモデルの読み込み後にコールバック関数を実行したい場合は、ml5.imageClassifier(?modelName, ?options, ?callback) にそれらを引数として渡すことができます。詳細は [ml5.imageClassifier() メゾンド](/reference/image-classifier?id=ml5imageclassifier) をご確認ください。 

<!-- 
### Load an image 
-->
### 画像をロードする

<!-- 
Next, let's load an image that we want to classify. Unfold the project directory by clicking the arrow `>` at the top left corner of the p5.js editor. Create a new folder called `images`. And upload a bird image named `bird.png` to the `images` folder. Remember to login to see this option. 
-->
次に、分類したい画像を読み込みます。p5.js エディタの左上にある`>`をクリックしてプロジェクトディレクトリを展開し、新しいフォルダ `images` を作成します。そこに `bird.png` という名前の鳥の画像を`images`フォルダにアップロードしてください。ログインが必要な場合もありますので、忘れずに行ってください。 

<!-- 
We are ready to write the code to load the image that we just uploaded. Define a variable `img` to store the image. 
-->
アップロードした画像を読み込むコードを書き、画像を保存するための変数 `img` を定義します。 

```javascript
let img;
```

<!-- 
In the `preload` function, load the image using the `loadImage` function. 
-->
`preload` 関数内で、`loadImage` 関数を使用して画像をロードします。 

```javascript
function preload() {
  classifier = ml5.imageClassifier("MobileNet");
  img = loadImage("images/bird.png");
}
```

<!-- 
### Classify the image with the model 
-->
### モデルで画像を分類する 

<!-- 
Within the `setup` function, call the `classify` method on the `classifier` object to - you guessed right - classify the image. The `classify` method takes the image and a callback function as parameters. 
-->
`setup` 関数内で、`classifier` オブジェクトの `classify` メソッドを呼び出して画像を分類します。`classify` メソッドは、画像とコールバック関数をパラメータとして受け取ります。 

```javascript
function setup() {
  createCanvas(400, 400);
  classifier.classify(img, gotResult);
}
```

<!-- 
The callback function `gotResult` is a function that will be called when the `classify` method finishes classifying the image. Now, let's define the `gotResult` function. 
-->
コールバック関数 `gotResult` は、`classify` メソッドが画像の分類を終了したときに呼び出される関数です。それでは、`gotResult` 関数を定義してみましょう。 

```javascript
// Callback function for when classification has finished
// 分類が終了したときに呼び出されるコールバック関数 
function gotResult(results) {
  // The results are in an array ordered by confidence
  // 結果は信頼度順に配列で返されます 
  console.log(results);
}
```

<!-- 
### Display the results 
-->
### 結果を表示する 

<!-- 
We need to first display the image itself on the canvas. Add the following code to the `setup` function. 
-->
まず、キャンバス上に画像自体を表示する必要があります。以下のコードを `setup` 関数に追加してください。 

```javascript
function setup() {
  // ...
  classifier.classify(img, gotResult);
  image(img, 0, 0, width, height);
}
```

<!-- 
We can then display the classification results on the canvas. With `fill()`, `stroke()`, and `textSize()`, we can set up the text style. 
-->
次に、分類結果をキャンバス上に表示します。`fill()`、`stroke()`、`textSize()` を使って、テキストスタイルを設定できます。 

```javascript
// 分類が終了したときのコールバック関数 
function gotResult(results) {
  // 結果は信頼度順に配列で返されます
  console.log(results);

  // キャンバス上に結果を表示 
  fill(255);
  stroke(0);
  textSize(18);
```

<!-- 
Let's get the top 1 label that model feels most confident about. `results[0]` is the object with the highest confidence score. We can then extract the label and confidence from this object. `nf()` is used to format the confidence score to two decimal places. 
-->
モデルの信頼度が一番高いラベルを取得しましょう。results[0] は信頼度が一番高いオブジェクトです。このオブジェクトからラベルと信頼度を取得できます。nf() を使用して、信頼度スコアを小数点以下2桁（ふたけた ）に揃えます。 

```javascript
label = "Label: " + results[0].label;
confidence = "Confidence: " + nf(results[0].confidence, 0, 2);
```

<!-- 
Finally, display the label and confidence on the canvas. 
-->
最後に、キャンバス上にラベルと信頼度を表示します。 

```javascript
  text(label, 10, 360);
  text(confidence, 10, 380);
}
```

<!--
### Run your sketch
-->
### スケッチを実行する

<!-- 
Voila! You have successfully built the ImageClassifier Single Image example. Press the <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `run` button to see the code in action. You can also find the [complete code](https://editor.p5js.org/ml5/sketches/pjPr6XmPY) in the p5.js web editor. 
-->
できました！ImageClassifier の単一画像の例の構築に成功しました！<img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `実行`ボタンを押してコードの動作を見てみましょう。[完全なコード](https://editor.p5js.org/ml5/sketches/pjPr6XmPY)はp5.jsウェブエディターでも確認できます。

<!--
?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better.
-->
?> この段階的なコードガイドで質問や不明点がございましたら、ぜひご連絡ください。[Discord](https://discord.com/invite/3CVauZMSt7)に参加して、改善点をお知らせください。

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
  - 使用するモデルの名前。通常は "mobilenet"、"darknet"、"darknet-tiny"、"doodlenet" のいずれか。
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
  - カスタムモデルを使用する場合のモデルの URL。
- **型**
  - String

---

### imageClassifier.model

<!-- 
- **Description**
  - The TensorFlow.js model used for image classification.
- **Type**
  - tf.LayersModel 
  -->
- **説明**
  - 画像分類に使用される TensorFlow.js モデル。
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
  - 使用する特定のモデルモジュール（例：MobileNet、Darknet、Doodlenet）。
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
  - カスタムモデルのラベルをインデックスにマッピングする配列。
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
  - 使用するモデルのバージョン（MobileNet に適用）。
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
  - 使用するモデルの α 値（幅倍率、MobileNet に適用）。
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
  - 返される上位の予測数（MobileNet に適用）。
- **型**
  - Number

---

### imageClassifier.isClassifying

<!-- 
- **Description**
  - A flag indicating whether the classification loop is currently running.
- **Type**
  - Boolean 
  -->
- **説明**
  - 現在、分類ループが実行中かどうかを示すフラグ。
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
  - 分類ループを停止するためのフラグ。
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
  - classifyStart または classifyStop の前回の呼び出しを記録し、警告を処理するために使用。
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
  - モデルが読み込まれたときに解決される Promise。
- **型**
  - Promise


<!-- 
## Methods 
-->
## メソッド

### ml5.imageClassifier()

<!-- 
This method is used to initialize the imageClassifer object. 
-->
このメソッドは、ImageClassifier オブジェクトを初期化するために使用されます。 

```javascript
const classifier = ml5.imageClassifier(modelNameOrUrl, ?options, ?callback);
```

**Parameters:**

<!-- 
- **modelName**: Optional.
  - String: Name of the underlying model to use. Possible values are `mobilenet`, `darknet` (28 MB in size), `darknet-tiny` (4 MB), `doodlenet`, or a URL to a compatible model file. -->
- **modelName**: オプション。
  - String: 使用するモデルの名前。指定可能な値は以下の通りです：mobilenet,darknet（サイズ: 28 MB）,darknet-tiny（サイズ: 4 MB）,doodlenet,互換性のあるモデルファイルへのURL。 

- **options**: オプション。
  - Object: モデルのデフォルト設定を変更するためのオブジェクト。

    <!-- 
    The default options for the default `mobilenet` model are 
    -->
    デフォルトの mobilenet モデルのオプションは以下の通りです。 

    ```
    {
      alpha: 1.0,
      topk: 3
    }
    ```
    <!-- 
    - _version_: The MobileNet version to use. Default is 2.
    - _alpha_: The width multiplier for the MobileNet. Default is 1.0.
    - _topk_: The number of labels to return. Default is 3. 
    -->
    - _version_: 使用する MobileNet のバージョン。デフォルトは 2。 
    - _alpha_: MobileNet の幅を調整するための倍率。デフォルトは 1.0。 
    - _topk_: 返されるラベル数。デフォルトは 3。

<!-- 
- **callback(classifier, error)**: Optional. A function to run once the model has been loaded. Alternatively, call `ml5.imageClassifier()` within the p5 `preload` function. 
-->
- **callback(classifier, error)**: オプション。モデルの読み込みが完了した際に実行される関数。または、p5 の preload 関数内で ml5.imageClassifier() を呼び出すことも可能です。

<!-- 
**Returns:**  
-->
**返り値:** 

<!-- 
The imageClassifier object. 
-->
imageClassifier オブジェクト。 

--- 

### imageClassifier.classifyStart()

<!-- 
This method repeatedly outputs classification labels on an image media through a callback function. 
-->
このメソッドは、コールバック関数を通じて、画像メディア上の分類ラベルを繰り返し出力します。 

```javascript
imageClassifier.classifyStart(media, ?kNumber, callback);
```

<!-- 
**Parameters:** 
-->
**パラメータ:**

<!-- 
- **media**: An HTML or p5.js image, video, or canvas element to run the classification on.

- **kNumber**: The number of labels returned by the image classification.

- **callback(results, error)**: A callback function to handle the output of the classification. See below for an example output passed into the callback function: 
-->
- **media**: 分類を実行するための HTML または p5.js の画像、ビデオ、またはキャンバス要素。 

- **kNumber**: 画像分類によって返されるラベルの数。

- **callback(results, error)**: 分類結果を処理するためのコールバック関数。コールバック関数に渡される出力例は以下の通り： 

  ```javascript
  [
    {
      label: "zebra",
      confidence: 0.98,
    },
    {
      label: "tiger",
      confidence: 0.89,
    },
    // 他のオブジェクトが続きます... 
  ];
  ```

---

### imageClassifier.classifyStop()

<!-- 
This method can be called after a call to `imageClassifier.classifyStart` to stop the repeating classifications. 
-->
このメソッドは、`imageClassifier.classifyStart` を呼び出した後に、繰り返される分類処理を停止するために使用されます。 

```javascript
imageClassifier.classifyStop();
```

--- 

### imageClassifier.classify()

<!-- 
This method asynchronously outputs a single image classification on an image media when called. 
-->
このメソッドは、画像メディアから1回だけ顔を検出して結果を返します（非同期的に動作します）。 

```javascript
imageClassifier.classify(media, ?kNumber, ?callback);
```

<!-- 
**Parameters:** 
-->
**パラメータ:** 

<!-- 
- **media**: An HTML or p5.js image, video, or canvas element to run the classification on.

- **kNumber**: The number of labels returned by the image classification.

- **callback(results, error)**: Optional. A callback function to handle the output of the classification. 
-->
- **media**: 分類を実行するための HTML または p5.js の画像、ビデオ、またはキャンバス要素。
- **kNumber**: 画像分類によって返されるラベルの数。
- **callback(results, error)**: オプション。分類結果を処理するためのコールバック関数。

<!-- 
**Returns:**  
-->
**返り値:** 

<!-- 
A promise that resolves to the estimation output. 
-->
分類結果を解決する promise を返します 
