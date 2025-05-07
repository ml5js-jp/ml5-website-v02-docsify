# SoundClassifier

<center>
  <img class="header-img" src="assets/header-sound-classifier.png" alt="SoundClassifier Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/kantortegalsari/" target="_blank" title="Kantor Tegalsari">Kantor Tegalsari</a> | <a href='mailto:info@ml5js.org'>Contribute \CID{206}</a> </p>
</center>

## 概要

<!--
SoundClassifier is a machine-learning model that allows you to classify audio.
-->
音声分類器は、音声を分類することのできる機械学習モデルです。 

<!--
It provides the following functionalities:
-->
このモデルは以下の機能を提供します。 

<!--
- **Sound identification**: Detect whether a certain noise (e.g., clapping) was made or a certain word (e.g., up, down) was said.
- **Custom models**: Flexibility to use [TensorFlow's SpeechCommands18w](https://github.com/tensorflow/tfjs-models/tree/master/speech-commands) model or your own custom pre-trained speech commands.
-->
- **音声の識別**: 特定の音（例えば、拍手）が鳴ったか、特定の単語（例えば、「上」、「下」）が発せられたかを検出します。
- **カスタムモデル**: TensorFlow's SpeechCommands18wモデルや、独自の事前トレーニング済みの音声コマンドを使用することができるという柔軟性があります。

<!--
The SpeechCommands18w model can recognize 18 sounds which include the ten digits from "zero" to "nine", "up", "down", "left", "right", "stop", "go", "yes", and "no". It also includes the categories "background noise" and "unknown".

If opting to train your own model, try [Google's Teachable Machine](https://teachablemachine.withgoogle.com).
-->
The SpeechCommands18wモデルは、「０」から「９」までの10種の数字や「上」、「下」、「左」、「右」、「ストップ」、「ゴー」、「はい」、「いいえ」を含む 18 種類の音を識別できます。また、"background noise" と "unknown"というカテゴリーも含まれます。 
独自のモデルをトレーニングする場合は、\UTF{202F}Google's Teachable Machineをお試しください。 

<!--
## Quick Start
-->
## クイックスタート！

<!--
Run and explore a pre-built example! [This SoundClassifier example](https://editor.p5js.org/ml5/sketches/HUm7NYMW3) recognizes speech commands using SpeechCommands18w.
-->
構築済みの例を実行してみましょう。 
この音声分類器の例はSpeechCommands18wを使用して音声コマンドを識別します。 

</br>

[DEMO](iframes/sound-classifier ":include :type=iframe width=100% height=550px")

<!--
## Examples
-->
## サンプル

<!--
- [SoundClassifier Speech Commands](https://editor.p5js.org/ml5/sketches/HUm7NYMW3): Sound classification using the SpeechCommands18w model.
- [SoundClassifier Teachable Machine](https://editor.p5js.org/ml5/sketches/mXeiNXSTU): Sound classification using a custom model with Google's Teachable Machine.
-->
- [SoundClassifier Speech Commands](https://editor.p5js.org/ml5/sketches/HUm7NYMW3): SpeechCommands18wを使用した音声分類。
- [SoundClassifier Teachable Machine](https://editor.p5js.org/ml5/sketches/mXeiNXSTU): GoogleのTeachable Machineによるカスタムモデルを使用した音声分類。

<!--
## Step-by-Step Guide
-->
## 段階的なガイド

<!--
Let's build the [Sound Classification example](https://editor.p5js.org/ml5/sketches/HUm7NYMW3) from scratch, and in the process, learn how to use SoundClassifier!
-->
ゼロからSound Classification example\UTF{202F}を構築し、その過程で音声分類器の使用方法を学びましょう。 

<!--
### Create a new project
-->
### 新しいプロジェクトを作成する

<!--
To follow along, start by creating an empty project in the [p5.js web editor](https://editor.p5js.org/).
-->
手順に従い、まず\UTF{202F}[p5.js web editor](https://editor.p5js.org/)で空のプロジェクトを作成します。 

<!--
### Set up ml5.js
-->
### ml5.jsのセットアップ

<!--
Import the ml5.js library in your `index.html` file.
-->
`index.html`ファイルにml5.jsライブラリーをインポートします。 

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
Let's open the `sketch.js` file and define a variable to store the SoundClassifier model.
-->
`sketch.js`ファイルを開き、センチメントモデルを保存する変数を定義しましょう。 

```javascript
let classifier;
```

<!--
Next, we will store the 18 words available in the SpeechCommands18w model in an array.
-->
次に、SpeechCommands18wモデルで使用可能な18の単語を配列に保存します。 

```javascript
let words = [
  "zero",
  "one",
  "two",
  "three",
  "four",
  "five",
  "six",
  "seven",
  "eight",
  "nine",
  "up",
  "down",
  "left",
  "right",
  "go",
  "stop",
  "yes",
  "no",
];
```
<!--
We're now going to create a `preload` function to load the SoundClassifier model. The `preload` function is a p5.js function that runs before the `setup` and `draw` function. This is where we load the model to ensure it is ready before we use it.

In this, we first create an `options` object to customize the model's behavior. For example, we can set the probability threshold, with the default being 0.
-->
ここで、音声分類器モデルをロードする$preload$関数を作成します。 $preload$関数は$setup$関数と$draw$関数の前に実行される$p5.js$関数です。 ここでモデルをロードし、使用前に準備ができていることを確認します。 
ここでは、まずモデルの挙動をカスタマイズするための$option$オブジェクトを作成します。例えば、デフォルトは0となっている確率の閾値を設定できます。

 
 

```javascript
function preload() {
  let options = { probabilityThreshold: 0.7 };

```

?> If you would like to know more about the available configuration settings for `options`, please check out the [Methods](/reference/sound-classifier?id=methods) section.


<!--
Now, we are ready to load a model configured as `options` specifies and store it in the `classifier` variable.
-->
これで、指定された$option$通りに設定されたモデルをロードし、$classifier$変数に保存する準備ができました。 

```javascript
  classifier = ml5.soundClassifier("SpeechCommands18w", options);
}
```
<!--
### Classify sound with the model
-->
### モデルを用いた音声分類

<!--
Define a variable to store the label of the classified sound.
-->
分類された音声のラベルを保存する変数を定義します。 

 
```javascript
// Variable for displaying the results on the canvas
let predictedWord = "";
```

<!--
Within the `setup` function, we call the `classifyStart` method on the `classifier` object to classify the sound. The `classifyStart` method takes a callback function as a parameter.
-->
$setup$関数内にて、 $classifier$オブジェクト上で$classifyStart$メソッドを呼び出し、音声を分類します。$classifyStart$メソッドはコールバック関数をパラメータとして受け取ります。


```javascript
function setup() {
  createCanvas(650, 450);
  // Classify the sound from microphone in real time
  classifier.classifyStart(gotResult);
}
```

<!--
Now, let's define the `gotResult` function. The callback function `gotResult` is a function that will be called when the `classifyStart` method finishes classifying the sound.
-->
それでは、$gotResult$関数を定義しましょう。コールバック関数である$gotResult$は、$classifyStart$メソッドが音声の分類を完了した時に呼び出される関数です。

```javascript
// A function to run when we get any errors and the results
function gotResult(results) {
  // The results are in an array ordered by confidence
  console.log(results);
```

<!--
Let's get the top 1 label that model feels most confident about. `results[0]` is the object with the highest confidence score.
-->
モデルが最も信頼している１つのラベルを取得しましょう。$results$0$$は信頼スコアが最も高いオブジェクトです。 


```javascript
  // Load the first label to the text variable displayed on the canvas
  predictedWord = results[0].label;
}
```
<!--
### Set up UI for user interaction
-->
### ユーザーインタラクションのためのUI を設定する

<!--
To give the user some guidance on how to interact with the model, we can add a prompt message. Let's define a function `displayWords()` to show the 18 words from the model on the canvas.
-->
モデルとの対話方法に関するガイダンスをユーザーへ提供するために、プロンプトメッセージを追加することができます。キャンバス上にモデルによる18の単語を表示する関数$displayWords()$を定義しましょう。

<!--
Using `textAlign()`, `textSize()`, and `fill()`, we can set up the text style.
-->
\UTF{202F}$textAlign()$、$textSize()$、$fill()$を使用して、テキストスタイルを設定できます。


```javascript
// Function to display the 18 words on the canvas
function displayWords() {
  textAlign(CENTER, CENTER);
  textSize(32);
  fill(96);
  text("Say one of these words!", width / 2, 40);
```

<!--
We can also specify where we want the words to appear on the screen. To set up rows and columns, we iterate all words of the `words` array, fetch the `i`th dectected word, and display it on the canvas.
-->
単語を画面上のどこに表示するかを指定することもできます。行と列を設定するためには、$words$配列の全ての単語を反復し、$i$番目に検出された単語を取り出し、キャンバス上に表示します。


```javascript
  let x = 125;
  let y = 150;
  // Words appear in 3 columns of 6 rows
  for (let i = 0; i < words.length; i++) {
    fill(158);
    text(words[i], x, y);
    y += 50;
    if ((i + 1) % 6 === 0) {
      x += 200;
      y = 150;
    }
  }
}
```
<!--
### Display the results
-->
### 結果を表示する

<!--
In the `draw()` function, draw the `background` and call the `displayWords()` function to display the 18 words.
-->
$draw()$関数内で、$background$を描画し、$displayWords()$関数を呼び出して18の単語を表示します。

```javascript
function draw() {
  background(250);
  // Call function for displaying background words
  displayWords();
```
<!--
Finally, we display the classification results on the canvas and again, use `fill()`, `textAlign()`, and `textSize()` to set up styling.
-->
最後に、分類結果をキャンバスに表示し、$fill()$,\UTF{202F}$textAlign()$,$textSize()$を再度使用してスタイルを設定します。

```javascript
  // Once the model outputs results start displaying the predicted word on the canvas
  if (predictedWord !== "") {
    fill(211, 107, 255);
    textAlign(CENTER, CENTER);
    textSize(64);
    text(predictedWord, width / 2, 90);
  }
}
```

<!--
### Run your sketch
-->
### スケッチを実行する

<!--
Voila! You have successfully built the Sound Classification example. Press the <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `run` button to see the code in action. You can also find the [complete code](https://editor.p5js.org/ml5/sketches/HUm7NYMW3) in the p5.js web editor.
-->
音声分類の例を構築することができました。コードの動作を見るためには実行ボタンを押してください。p5.jsのwebエディターで[完全なコード](https://editor.p5js.org/ml5/sketches/hopIvsCGL)を確認することもできます。 


<!--
?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better.
-->
?> この段階的なコードガイドで質問や不明点がございましたら、ぜひご連絡ください。[Discord](https://discord.com/invite/3CVauZMSt7)に参加して、改善点をお知らせください。


<!--
## Properties
-->
## プロパティ
### SoundClassifier Properties


#### soundClassifier.model

- **Description**:
  - The loaded model instance. Initially set to `null` and assigned after the model is loaded.
- **Type**:
  - Object | Null

---

#### soundClassifier.options

- **Description**:
  - Configuration options provided during initialization. These options control the behavior and performance of the model.
- **Type**:
  - Object

---

#### soundClassifier.isClassifying

- **Description**:
  - A flag indicating whether the classification loop is currently running. It is set to `true` when classification is in progress and `false` otherwise.
- **Type**:
  - Boolean

---

#### soundClassifier.signalStop

- **Description**:
  - A flag used to signal the classification loop to stop. It is set to `true` to stop the classification process.
- **Type**:
  - Boolean

---

#### soundClassifier.prevCall

- **Description**:
  - Tracks the previous call to detect if `classifyStart` or `classifyStop` was called. Helps manage the state of the classifier.
- **Type**:
  - String

---

#### soundClassifier.modelName

- **Description**:
  - The name of the model to use. It is set based on the provided `modelNameOrUrl` parameter during initialization.
- **Type**:
  - String | Null

---

#### soundClassifier.modelUrl

- **Description**:
  - The URL of the model to use. It is set based on the provided `modelNameOrUrl` parameter during initialization.
- **Type**:
  - String | Null

---

#### soundClassifier.modelToUse

- **Description**:
  - The specific model module to use (e.g., `speechCommands`). It is determined based on the `modelName`.
- **Type**:
  - Object | Null

---

#### soundClassifier.ready

- **Description**:
  - A promise that resolves when the model is successfully loaded and ready to be used. This ensures the model is fully prepared before any classification starts.
- **Type**:
  - `Promise`

<!--
## Methods
-->
## メソッド

### ml5.soundClassifier()

<!--
This method is used to initialize the soundClassifier object.
-->
このメソッドは、soundClassifierオブジェクトを初期化するために使用されます。

```js
let soundclassifier = ml5.soundClassifier(?model, ?options, ?callback)
```
<!--
**Parameters:**
-->
**パラメータ:**

<!--
- **model**: Optional. Model name or URL path to a `model.json`. Here are some options:
  - `SpeechCommands18w`: loads the 18w speech commands
    ```js
    let classifier = ml5.soundClassifier("SpeechCommands18w", modelReady);
    ```
  - Custom model made in Google's Teachable Machine:
    ```js
    let classifier = ml5.soundClassifier("path/to/model.json", modelReady);
    ```
- **options**: Optional. An object describing a model accuracy and performance.
  The default and available options are:
-->
- **モデル**: オプション. モデル名または `model.json`へのURLパス。以下のようなオプションがあります:
  - `SpeechCommands18w`: 18wの音声コマンドモデルを読み込む
    ```js
    let classifier = ml5.soundClassifier("SpeechCommands18w", modelReady);
    ```
  -  Googleの Teachable Machineで作成したカスタムモデル:
    ```js
    let classifier = ml5.soundClassifier("path/to/model.json", modelReady);
    ```
- **オプション**: オプション. モデルの精度とパフォーマンスを指定するオブジェクト。
  デフォルトのオプションと利用可能なオプションは以下の通りです:



  ```js
  {
    overlapFactor: 0.5,
    includeSpectrogram: false,
    probabilityThreshold: 0,
    invokeCallbackOnNoiseAndUnknown: false,
    includeEmbedding: false
  };
  ```

  Options include:

  - **overlapFactor** - Optional
    - Number: Controls how often the recognizer performs prediction on spectrograms. Must be >=0 and <1 (default: 0.5). For example, if each spectrogram is 1000 ms long and overlapFactor is set to 0.25, the prediction will happen every 250 ms.
  - **includeSpectrogram** - Optional
    - Boolean: Let the callback function be invoked with the spectrogram data included in the argument. Default: false
  - **probabilityThreshold** - Optional
    - Number: The callback function will be invoked if and only if the maximum probability score of all the words is greater than this threshold. Default: 0.
  - **invokeCallbackOnNoiseAndUnknown** - Optional
    - Boolean: Whether the callback function will be invoked if the "word" with the maximum probability score is the "unknown" or "background noise" token. Default: false.
  - **includeEmbedding** - Optional
    - Boolean: Whether an internal activation from the underlying model will be included in the callback argument, in addition to the probability scores. Note: if this field is set as true, the value of invokeCallbackOnNoiseAndUnknown will be overridden to true and the value of probabilityThreshold will be overridden to 0.

  (credit: [TensorFlow.js](https://www.npmjs.com/package/@tensorflow-models/speech-commands))

  - **callback**: Optional. A function to run once the model has been loaded. Alternatively, call `ml5.soundClassifier()` within the p5 `preload` function.

---

### soundClassifier.classifyStart()

This method repeatedly outputs classification labels on an audio media through a callback function.

```js
soundClassifier.classifyStart(numOrCallback, callback);
```

**Parameters:**

- **numOrCallback:** Optional. A number representing the number of classes to classify or a callback function to handle the results. If no number is provided, the default is the length of the labels in the model.
- **callback:** Optional. A function to handle the classification results. The callback function will receive an array of objects with the following structure:

  ```js
  [
    {
      label: "up",
      confidence: 0.92,
    },
    {
      label: "down",
      confidence: 0.05,
    },
    // Additional objects here...
  ];
  ```

  **Returns:**

- **Promise:** If no callback is provided, the method returns a promise that resolves when the classification process starts and provides the classification results.
- **Callback Results:** If a callback is provided, the results are passed directly to the callback function.

---

### soundClassifier.classifyStop()

This method can be called after a call to `soundClassifier.classifyStart` to stop the repeating classifications.

```js
soundClassifier.classifyStop();
```

**Returns:**
None