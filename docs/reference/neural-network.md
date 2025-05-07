# NeuralNetwork

<center>
  <img class="header-img" src="assets/header-neural-network.png" alt="NeuralNetwork Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/lutfidiarycoc/" target="_blank" title="LUTFI GANI AL ACHMAD">LUTFI GANI AL ACHMAD</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

## 説明
<!-- The ml5.js Neural Network allows you to create and train your own machine learning models in the browser. You can use the neural network to perform classification tasks, where the model predicts a label based on the input data, or regression tasks, where the model predicts a value based on the input data.  -->
ml5.jsのニューラルネットワークは、ブラウザ上で独自の機械学習モデルを作成し、訓練することができます。 ニューラルネットワークを使用すると、入力データに基づいてラベルを予測する分類タスクや、入力データに基づいて値を予測する回帰タスクを実行できます。  
<!-- The neural network is a type of machine learning model that is inspired by the human brain. It is made up of layers of neurons that are connected to each other. Each neuron takes in input data, processes it, and passes the output to the next layer of neurons. The neural network learns by adjusting the weights of the connections between neurons to minimize the error in its predictions. -->
ニューラルネットワークは、人間の脳にヒントを得た機械学習モデルの一種です。 互いに接続されたニューロンの層で構成されています。 各ニューロンは入力データを受け取り、処理し、出力を次の層のニューロンに渡します。 ニューラルネットワークは、ニューロン間の接続の重みを調整することで、予測の誤差を最小化して学習します。
<!-- It provides folowing functionalities:
- **Classification**: The neural network can be used to classify input data into different categories. For example, you can train a neural network to classify images of cats and dogs.
- **Regression**: The neural network can be used to predict a continuous value based on input data. For example, you can train a neural network to predict the price of a house based on its size and location. -->
ニューラルネットワークは次のような機能を提供します：  
- **分類**： ニューラルネットワークは入力データを異なるカテゴリーに分類するために使用できます。 例えば、ネコとイヌの画像を分類するためにニューラルネットワークをトレーニングすることができます。  
- **回帰**： ニューラルネットワークは、入力データに基づいて連続値を予測するために使用できます。 例えば、ニューラルネットワークを訓練して、家の大きさと場所に基づいて家の価格を予測することができます。 

<!-- ?> If you are not familiar with the concept of **classification**, **regression**, **neuron**, **neural networks**, and **weights**, you can learn more about them with [ml5 glossary](/glossary). -->
?> **分類**, **回帰**, **ニューロン**, **ニューラルネットワーク**,**重み**の概念に馴染みがない場合は、 [ml5 glossary](/glossary)で詳しく学ぶことができます。
<!-- ## Quick Start
Run and explore a pre-built example! [This Neural Network example](https://editor.p5js.org/ml5/sketches/eGHBdmCLe) trains a model to classify the color of an RGB value. -->

## クイックスタート
事前に構築されたサンプルを実行して探索します！ [このニューラルネットワークの例](https://editor.p5js.org/ml5/sketches/eGHBdmCLe)は、RGB値の色を分類するモデルを学習します。 
</br>

[DEMO](iframes/neural-network ":include :type=iframe width=100% height=550px")

<!-- ## Examples
- [NeuralNetwork Color Classifier](https://editor.p5js.org/ml5/sketches/eGHBdmCLe): Train a model to classify the color of an RGB value (red-ish, green-ish, blue-ish).
- [NeuralNetwork Mouse Gesture](https://editor.p5js.org/ml5/sketches/FdXAgrA3N): Train a model to recognize mouse gestures (up, down, left, right).
- [NeuralNetwork Load Model](https://editor.p5js.org/ml5/sketches/U-aljtx7x): Load a pre-trained model and use it for classification.
- [NeuralNetwork Train and Save](https://editor.p5js.org/ml5/sketches/rR51vvi-u): Train a model and save it for later use. -->

## 例
- [NeuralNetwork Color Classifier](https://editor.p5js.org/ml5/sketches/eGHBdmCLe): RGB値の色（赤っぽい、緑っぽい、青っぽい）を分類するモデルを学習します。  
- [NeuralNetwork Mouse Gesture](https://editor.p5js.org/ml5/sketches/FdXAgrA3N): マウスのジェスチャー（上、下、左、右）を認識するモデルを学習します。 
- [NeuralNetwork Load Model](https://editor.p5js.org/ml5/sketches/U-aljtx7x): 事前にトレーニングされたモデルをロードし、分類に使用します。  
- [NeuralNetwork Train and Save](https://editor.p5js.org/ml5/sketches/rR51vvi-u): モデルをトレーニングし、後で使用するために保存します。 

<!-- ## Step-by-Step Guide
This step-by-step guide uses a p5.js sketch running on the [p5.js web editor](https://editor.p5js.org/). To follow along, start by creating an empty project in the editor.

### Set up ml5.js

Import the ml5.js library in your `index.html` file by copying the following `<script>` tag. -->

## ステップバイステップガイド 
このステップバイステップのガイドでは、[p5.jsウェブエディタ](https://editor.p5js.org/)上で動作するp5.jsスケッチを使用します。 まず、エディタで空のプロジェクトを作成します。

### ml5.jsのセットアップ  
以下の<script>タグをコピーして、`index.html`ファイルにml5.jsライブラリをインポートします。 
```html
<script src="https://unpkg.com/ml5@1/dist/ml5.js"></script>
```

<!-- ?> If you are not familiar with how to import the ml5.js library and need more detailed guidance, please check out our [Getting Started](/?id=set-up-ml5js) tutorial.

### Initialize the model
First of all, create a variable `classifier` to store the neural network model. -->
?> ml5.jsライブラリのインポート方法がよくわからず、より詳細なガイダンスが必要な場合は、[Getting Started](/?id=set-up-ml5js)チュートリアルをご覧ください。

### モデルの初期化  
まず最初に、ニューラルネットワークモデルを格納するための変数'classifier'を作成します。 

```javascript
let classifier;
```

<!-- Let's then set up the backend to `webgl` to allow this example to work across all browsers in your `sketch.js` file. -->
次に、この例が`sketch.js`ファイルのすべてのブラウザで動作するように、バックエンドを`webgl`に設定しよう。 
```javascript
function setup() {
  createCanvas(640, 240);

  // Set the backend to 'webgl'
  ml5.setBackend("webgl");
```

<!-- Create a variable `options` to configure the model. -->
モデルを構成するための変数オプションを作成します。 
```javascript
  // Set the options for the neural network
  let options = {
    task: "classification",
    debug: true,
  };
```

<!-- Initialize the neural network model with the options. -->
オプションでニューラルネットワークモデルを初期化する。 
```javascript
  // Initialize the neural network
  classifier = ml5.neuralNetwork(options);
}
```
<!-- ?> If you would like to configure the model with greater flexibility (such as defining inputs and outputs, loading external data, or creating custom layers), refer to the [Methods](/reference/neural-network?id=methods) section for more details. -->
より柔軟にモデルを設定したい場合（入力と出力の定義、外部データの読み込み、カスタムレイヤーの作成など）、詳細は[メソッド](/reference/neural-network?id=methods)のセクションを参照してください。
<!-- ### Prepare training dataset
Different from other pre-trained ml5.js models, the ml5.js Neural Network allows you to train a custom model with your own data. You can create your own data or load data from a file. In this example, we will create our own data. In your `sketch.js` file, define an array of data that contains RGB values and their corresponding color labels. -->

### トレーニングデータセットを準備する  
他のトレーニング済みのml5.jsモデルとは異なり、ml5.js Neural Networkでは、独自のデータでカスタムモデルをトレーニングすることができます。 独自のデータを作成することも、ファイルからデータをロードすることもできます。 この例では、独自のデータを作成します。 `sketch.js`ファイルで、RGB値とそれに対応するカラー・ラベルを含むデータの配列を定義します。 

```javascript
let data = [
  { r: 255, g: 0, b: 0, color: "red-ish" },
  { r: 254, g: 0, b: 0, color: "red-ish" },
  { r: 253, g: 0, b: 0, color: "red-ish" },
  { r: 0, g: 255, b: 0, color: "green-ish" },
  { r: 0, g: 254, b: 0, color: "green-ish" },
  { r: 0, g: 253, b: 0, color: "green-ish" },
  { r: 0, g: 0, b: 255, color: "blue-ish" },
  { r: 0, g: 0, b: 254, color: "blue-ish" },
  { r: 0, g: 0, b: 253, color: "blue-ish" },
];
```

<!-- The model examines the RGB values (features) to understand which patterns correspond to specific labels. By learning these patterns, the model can accurately predict the label for new, unseen data based on the features it has been trained on.

?> If you would like to load data from a file, refer to the [Methods](/reference/neural-network?id=methods) section for more details.

Now, we will add the data to the neural network model. We iterate through the data array and store each sample to a variable `item`. -->
モデルはRGB値（特徴）を調べ、どのパターンが特定のラベルに対応するかを理解する。 これらのパターンを学習することで、モデルは学習した特徴に基づいて、新しい未見のデータのラベルを正確に予測できるようになります。 

?> ファイルからデータをロードしたい場合は、[メソッド](/reference/neural-network?id=methods)のセクションを参照してください。

次に、ニューラルネットワークモデルにデータを追加します。 データ配列を繰り返し処理し、各サンプルを変数`item`に格納します。
```javascript
function setup() {
  ...
  classifier = ml5.neuralNetwork(options);

  // Add data to the neural network
  for (let i = 0; i < data.length; i++) {
    let item = data[i];
```
<!-- We extract the RGB values of the sample, and generate three features: `r`, `g`, and `b`. -->
サンプルのRGB値を抽出し、 `r`, `g`, `b`の3つの特徴量を生成します。
```javascript
    let inputs = [item.r, item.g, item.b];
```

<!-- We also extract the color label of the sample and store it as the target output that model will predict. -->
また、サンプルのカラーラベルを抽出し、モデルが予測するターゲット出力として保存します。 
```javascript
    let outputs = [item.color];
```

<!-- Now, we can add the sample to the neural network model. -->
これで、ニューラルネットワーク・モデルにサンプルを追加できます。 
```javascript
    classifier.addData(inputs, outputs);
```

<!-- Lastly, normalize the data to ensure that the features are on a similar scale. -->
最後に、データが同じような尺度になるように正規化します。 
```javascript
  classifier.normalizeData();
}
```
<!-- ?> If you are not familiar with the concept of **normalization**, you can learn more about it with [ml5 glossary](/learn/ml5-glossary?id=normalization).

### Train the model
Now, we can train the neural network model with the training data. Define the training options, such as the number of epochs and batch size. -->
?> もし正規化という概念に馴染みがなければ、[ml5 glossary](/learn/ml5-glossary?id=normalization)で詳しく学ぶことができます。

### モデルを訓練する  
<!-- Now, we can train the neural network model with the training data. Define the training options, such as the number of epochs and batch size.  -->
さて、訓練データを使ってニューラルネットワークモデルを訓練することができます。 エポック数やバッチサイズなどのトレーニングオプションを定義します。 
```javascript
function setup() {
  ...
  classifier.normalizeData();

  // Train the neural network
  const trainingOptions = {
    epochs: 32,
    batchSize: 12,
  };
```

<!-- Train the model with `trainingOptions` and a callback function that is called when the training is finished. -->
`trainingOptions`とトレーニング終了時に呼び出されるコールバック関数でモデルをトレーニングします。
```javascript
  classifier.train(trainingOptions, finishedTraining);
}
```

<!-- ?> If you would like to configure the training process with greater flexibility (such as adding a callback function that is called after each epoch of training or when the training is finished), refer to the [Methods](/reference/neural-network?id=methods) section for more details.

Now, define the callback function `finishedTraining` that will be called when the training is finished. In our case, we will call the `classify()` function to make a classification on the test data once the model is trained. -->
?> より柔軟にトレーニングプロセスを設定したい場合（トレーニングの各エポック後またはトレーニング終了時に呼び出されるコールバック関数を追加するなど）、詳細については[メソッド](/reference/neural-network?id=methods)のセクションを参照してください。
次に、学習が終了したときに呼び出されるコールバック関数`finishedTraining`を定義します。 この例では、モデルの学習が完了したら、`classify()`関数を呼び出してテストデータの分類を行います。
```javascript
function finishedTraining() {
  classify();
}
```

<!-- ### Prepare test data -->

### テストデータの準備  

<!-- We can start by creating three variables to store the features `r`, `g`, and `b` of the test data. -->
まず、テストデータの特徴`r`, `g`,`b`を格納する3つの変数を作成する。
```javascript
let r = 255;
let g = 0;
let b = 0;
```

<!-- ?> Note in this example we only have one test sample, but you can have multiple test samples (e.g., an array of color samples) to classify. Please refer to the [Methods](/reference/neural-network?id=methods) section for more details.

Let's also create a `label` variable to store the predicted color label, and set it to "training" initially. This variable will be updated with the predicted label after the classification. -->
?> この例では1つのテストサンプルしかありませんが、複数のテストサンプル（例えば色サンプルの配列）を持って分類することもできます。 詳細については、[メソッド](/reference/neural-network?id=methods)のセクションを参照してください。

また、予測されたカラー・ラベルを格納する変数`label`を作成し、最初は "training "に設定しましょう。 この変数は、分類後に予測されたラベルで更新されます。 
```javascript
let label = "training";
```

<!-- If we keep the RGB values of the test data fixed as initially set, the model will always predict the color label "red-ish," since the test data is always {r: 255, g: 0, b: 0}. Let's add some interactivity by allowing users to change the RGB values of the test data using sliders.

We can create three sliders to control the values of `r`, `g`, and `b`. -->
テストデータのRGB値を初期設定のまま固定しておくと、テストデータは常に{r: 255, g: 0, b: 0}なので、モデルは常に"赤っぽい"というカラーラベルを予測します。 ユーザーがスライダーを使ってテストデータのRGB値を変更できるようにして、インタラクティブ性を追加してみましょう。

`r`, `g`, `b`の値をコントロールする3つのスライダーを作成できます。 
```javascript
let rSlider, gSlider, bSlider;
```

<!-- In the `setup()` function, create the sliders and set their initial values. The `createSlider()` function creates a slider with a range of values from 0 to 255 and an initial value of 255 for the red slider, 0 for the green slider, and 0 for the blue slider. -->

`setup()`関数でスライダーを作成し、初期値を設定します。 `createSlider()`関数は、0から255までの値の範囲を持つスライダーを作成し、赤スライダーの初期値を255、緑スライダーの初期値を0、青スライダーの初期値を0とします。 
```javascript
function setup() {
  ...
  ml5.setBackend("webgl");

  rSlider = createSlider(0, 255, 255).position(10, 20);
  gSlider = createSlider(0, 255, 0).position(10, 40);
  bSlider = createSlider(0, 255, 0).position(10, 60);

  ...
}
```

<!-- We would like to update the RGB values of the test data based on the slider values. In the `draw()` function, update the `r`, `g`, and `b` variables with the slider values. -->
スライダーの値に基づいてテストデータのRGB値を更新したいと思います。 `draw()`関数で、`r`, `g`, `b`変数をスライダーの値で更新します。

```javascript
function draw() {
  r = rSlider.value();
  g = gSlider.value();
  b = bSlider.value();
```

<!-- And update the background color of the canvas with the new RGB values. -->
そしてキャンバスの背景色を新しいRGB値で更新します。
```javascript
  background(r, g, b);
}
```

<!-- ### Make a classification on the test data
Now, we can make a classification on the test data using the `classify()` function. Remember we will call this function after the model is trained. -->

### テストデータで分類を行う  
さて、`classify()`関数を使ってテスト・データで分類を行います。 この関数はモデルが学習された後に呼び出すことを忘れないでください。 
```javascript
function finishedTraining() {
  classify();
}
```

<!-- Let's define the `classify()` function that will make a classification on the test data. The `classify()` function takes the input data `[r, g, b]` and a callback function `handleResults` that will be called when the classification is finished. -->
テスト・データの分類を行う`classify()`関数を定義しましょう。 `classify()`関数は、入力データ`[r, g, b]`と、分類が終了したときに呼び出されるコールバック関数 `handleResults` を受け取ります。 

```javascript
function classify() {
  const input = [r, g, b];
  classifier.classify(input, handleResults);
}
```

<!-- The `handleResults` function will be called after the classification is finished. It takes two arguments: `results` and `error`. If there is an error, we will log the error to the console. Otherwise, we will update the `label` variable with the predicted color label and call the `classify()` function again to make a classification on the new test data. -->
`handleResults`関数は、分類終了後に呼び出される。 引数は`results`と`error`の2つです。 もしエラーがあれば、そのエラーをコンソールに記録します。 そうでなければ、変数`label`を予測された色ラベルで更新し、`classify()`関数を再度呼び出して、新しいテストデータで分類を行います。 
```javascript
function handleResults(results, error) {
  if (error) {
    console.error(error);
    return;
  }
  label = results[0].label;
  // console.log(results); // {label: 'red', confidence: 0.8};
  classify();
}
```

<!-- ### Display the classification result
We know that the `label` variable stores the predicted color label. Let's display the predicted color label on the canvas. In the `draw()` function, add the following code to display the `label` in the center of the canvas. -->

### 分類結果を表示する 

変数`label`には予測されたカラーラベルが格納されていることが分かっています。 予測された色のラベルをキャンバスに表示してみましょう。 `draw()`関数の中に以下のコードを追加して、`label`をキャンバスの中央に表示します。
```javascript
function draw() {
  ...
  background(r, g, b);

  textAlign(CENTER, CENTER);
  textSize(64);
  text(label, width / 2, height / 2);
}
```

<!-- ### Run your sketch
Now you can run your sketch and interact with the sliders to change the RGB values of the test data. The canvas will display the predicted color label based on the RGB values you set. You can also find the [complete code](https://editor.p5js.org/ml5/sketches/eGHBdmCLe) in the p5.js web editor.

?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better. -->
### スケッチを実行する 

テストデータの RGB 値を変更するために、スケッチを実行し、スライダーを操作することができます。 キャンバスには、設定した RGB 値に基づいて予測されたカラー ラベルが表示されます。 [完全なコード](https://editor.p5js.org/ml5/sketches/eGHBdmCLe)はp5.jsウェブエディタにもあります。 

?> このステップバイステップのコードガイドで不明な点や質問があれば、ぜひお寄せください！ [Discord](https://discord.com/invite/3CVauZMSt7)
に参加して、より良いものにする方法を教えてください。

<!-- ## Properties -->

<!-- | property             | description                                                                             | datatype   |
| :------------------- | --------------------------------------------------------------------------------------- | ---------- |
| `.callback`          | the callback to be called after data is loaded on initialization                        | `function` |
| `.options`           | the options for how the neuralNetwork should be configured on initialization            | `object`   |
| `.neuralNetwork`     | the `neuralNetwork` class where all of the tensorflow.js model operations are organized | `class`    |
| `.neuralNetworkData` | the `neuralNetworkData` class where all of the data handling operations are organized   | `class`    |
| `.neuralNetworkVis`  | the `neuralNetworkVis` class where all of the tf-vis operations are organized           | `class`    |
| `.data`              | The property that stores all of the training data after `.train()` is called            | `class`    |
| `.ready`             | set to true if the model is loaded and ready, false if it is not.                       | `ブール値`  | -->

<!-- ## Methods -->

## メソッド
### 概要
| メソッド                | 説明                                                                                                                            |
| :-------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `.addData()`          | `neuralNetworkData.data.raw`配列にデータを追加する。                                                               |
| `.normalizeData()`    | `neuralNetworkData.data.raw`に格納されているデータを正規化し、正規化した値を`neuralNetwork.data.training`配列に格納する。 |
| `.train()`            | モデルを訓練するために、`neuralNetwork.data.training` 配列のデータを使用します。                                                           |
| `.predict()`          | 回帰タスクでは、入力配列またはJSONオブジェクトに基づいて予測を行うことができます。                                         |
| `.predictMultiple()`  | 回帰タスクでは、配列の入力配列またはJSONオブジェクトの配列に基づいて予測を行うことができます。                      |
| `.classify()`         | 分類タスクでは、入力配列またはJSONオブジェクトに基づいて分類を行うことができます。                            |
| `.classifyMultiple()` | 分類タスクでは、配列の入力配列またはJSONオブジェクトの配列に基づいて分類を行うことができます。               |
| `.saveData()`         | `neuralNetworkData.data.raw` 配列からデータを保存できます。                                     |
| `.loadData()`         | `.saveData()`関数で保存したデータをロードできます。                                                         |
| `.save()`             | 学習済みモデルを保存します。                                                                              |
| `.load()`             | 学習済みモデルをロードできます。                                                                                |
| `.mutate()`           | モデルの重みを変更できます。                                                                      |
| `.crossover()`        | crossover を使用して新しいニューラルネットワークを作成することができます。                                                              |

### ml5.neuralNetwork()

<!-- This method initializes the `neuralNetwork` object. -->
このメソッドはneuralNetworkオブジェクトを初期化します。 
```javascript
const nn = ml5.neuralNetwork(options, callback);
```

<!-- **Parameters:** -->
**パラメータ:**
<!-- - **options**: Required. An object to configure the neural network. The available options are: -->
- **オプション**:必須。 ニューラルネットワークを設定するオブジェクト。 利用可能なオプションは以下の通り： 
  ```javascript
  {
    inputs: [], // 数値にすることも出来る
    outputs: [], // 数値にすることも出来る
    dataUrl: null,
    modelUrl: null,
    layers: [], // カスタムレイヤー
    task: null, // 'classification', 'regression', 'imageClassification'
    debug: false, // トレーニングの視覚化を表示するかどうかを決定する
    learningRate: 0.2,
    hiddenUnits: 16,
  }
  ```
  - _inputs_ - オプション
    - 配列 | 数値: 入力ラベルを配列または入力数で表す。 デフォルトは[]。
  - _outputs_ - オプション
    - 配列 | 数値： ラベルを配列または出力数として出力する。 デフォルトは[]。
  - _dataUrl_ - オプション
    - 文字列: データを含むCSVまたはJSONファイルのURL。
  - _modelUrl_ - オプション
    - 文字列: 訓練済みモデルのURL。
  - _layers_ - オプション
    - 配列: ニューラルネットワークのカスタムレイヤー。
  - _task_ - Required
    - 文字列: タスクのタイプ: 'classification(分類)', 'regression(回帰)', 'imageClassification(画像分類)'.
  - _debug_ - オプション
    - ブール値: トレーニングの可視化を表示する。 デフォルトはfalse。
  - _learningRate_ - オプション
    - 数値: トレーニングの学習率。 デフォルトは0.2。 
  - _hiddenUnits_ - オプション
    - 数値: デフォルト・レイヤーの隠れユニット数。 デフォルトは16。

- **callback(nn)**: オプション.モデルが初期化されたら実行する関数。 

**戻り値:** 

- **オブジェクト**: ニューラルネットワークオブジェクト。 このオブジェクトには、データを追加し、データを正規化し、モデルを訓練し、予測を行うためのメソッドが含まれています。

---

### nn.addData()

<!-- This method adds data to the neural network. -->
このメソッドでは、ニューラルネットワークにデータを追加します。

```javascript
nn.addData(xs, ys);
```

<!-- **Parameters:** -->
**パラメータ:**

<!-- - **xs**: Required. 配列 | Object. Input data.
  - If an array is given, the inputs must be ordered as specified in the constructor. If no labels are given in the constructor, then the order that your data are added here will set the order of how you will pass data to `.predict()` or `.classify()`.
  - If an object is given, then feed in key/value pairs.
  - If an object is given, provide key/value pairs.
  - If task is `imageClassification`, provide an HTMLImageElement, HTMLCanvasElement, or a flat 1-D array of pixel values.
- **ys**: Required. 配列 | Object. Output data.
  - If an array is given, the outputs must be ordered as specified in the constructor.
  - If an object is given, provide key/value pairs. -->

- **xs**: 必須。 配列 | オブジェクト。入力データ。 
  - 配列が指定された場合、コンストラクタで指定された順序で入力する必要があります。コンストラクタでラベルが与えられていない場合、ここに追加されるデータの順序が、 `.predict()` や `.classify()` にデータを渡す順序となります。
  - オブジェクトが与えられている場合は、キーと値のペアを入力します。 
  - オブジェクトが与えられた場合は、キーと値のペアを与えます。 
  - タスクが `imageClassification` の場合は、HTMLImageElement、HTMLCanvasElement、またはピクセル値のフラットな1次元配列を指定します。
- **ys**: 必須。 配列 | オブジェクト。出力データ。 
  - 配列が指定された場合は、コンストラクタで指定された順序で出力されなければならない。 
  - オブジェクトが指定された場合は、キーと値のペアを指定します。

<!-- **Returns:** -->
**戻り値:**

<!-- - n/a: Adds data to `neuralNetworkData.data.raw`. -->
- n/a: データを `neuralNetworkData.data.raw` に追加します。
---

### nn.normalizeData()

このメソッドは、0 から 1 までの尺度でデータを正規化します。  

```javascript
nn.normalizeData();
```

<!-- **Parameters:** -->
**パラメータ:**

- n/a

<!-- **Returns:** -->
**戻り値:**

<!-- - n/a: normalizes the data in `neuralNetworkData.data.raw` and adds `inputs` and `output` tensors to `neuralNetworkData.data.tensor` as well as the `inputMin`, `inputMax`, `outputMin`, and `outputMax` as tensors. The `inputMin`, `inputMax`, `outputMin`, and `outputMax` are also added to `neuralNetworkData.data` as Numbers. -->
- n/a: `neuralNetworkData.data.raw` のデータを正規化し、`neuralNetworkData.data.tensor` に `inputMin`, `inputMax`, `outputMin`, `outputMax` をテンソルとして追加する。`inputMin`, `inputMax`, `outputMin`, `outputMax` も数値として `neuralNetworkData.data` に追加される。 
---

### nn.train()

<!-- This method trains the model with the data loaded during the instantiation or added using `.addData()`. -->
このメソッドは、インスタンス生成時にロードされたデータ、または `.addData()` を使用して追加されたデータを使用してモデルを学習します。 
```javascript
nn.train(?optionsOrCallback, ?optionsOrWhileTraining, ?callback);
```

<!-- **Parameters:** -->
**パラメータ:**

<!-- - **optionsOrCallback**: オプション.
  - If an object of options is given, specify `batchSize` and `epochs`:
    ```javascript
    {
      batchSize: 24,
      epochs: 32,
    }
    ```
  - If a callback function is given, it will be called when the training is finished.
- **optionsOrWhileTraining**: オプション.
  - If an object of options is given as the first parameter, specify a callback function to be called when the training is finished.
- **callback**: オプション. Function.
  - If an object of options is given as the first parameter and a callback function is given as a second parameter, then this `callback` parameter will be a callback function that is fired after the training as finished. -->

**optionsOrCallback**: オプション.
  - オプションのオブジェクトが与えられた場合、`batchSize`と`epochs`を指定する：
    ```javascript
    {
      batchSize: 24,
      epochs: 32,
    }
    ```
  - コールバック関数が与えられた場合、トレーニングが終了したときに呼び出されます。
- **optionsOrWhileTraining**: オプション.
  - オプションのオブジェクトが最初のパラメータとして与えられた場合、トレーニングが終了したときに呼び出されるコールバック関数を指定します。
- **callback**: オプション. 関数
  - オプションのオブジェクトが最初のパラメータとして指定され、コールバック関数が2番目のパラメータとして指定された場合、この`callback`パラメータはトレーニング終了後に呼び出されるコールバック関数となります。 
  ```js
  const trainingOptions = {
    batchSize: 32,
    epochs: 12,
  };
  function whileTraining(epoch, loss) {
    console.log(`epoch: ${epoch}, loss:${loss}`);
  }
  function doneTraining() {
    console.log("done!");
  }
  neuralNetwork.train(trainingOptions, whileTraining, doneTraining);
  ```

<!-- **Returns:** -->
**戻り値:**

<!-- - n/a: Creates and trains the `nn.model`. -->
- n/a: nn.modelを作成し、学習させます。 
---

### nn.predict()

<!-- This method returns an array of predictions for the given input. -->
このメソッドは、与えられた入力に対する予測値の配列を返します。
```javascript
nn.predict(inputs, callback);
```

<!-- **Parameters:** -->
**パラメータ:**

<!-- - **inputs**: Required. Array | Object. Input values.
  - If an array is given, match the order specified in the constructor options.
  - If an object is given, provide key/value pairs matching the keys specified in the constructor options.
- **callback(results)**: Required. Function. A function to handle the results of `.predict()`.

**Returns:**

- **Array**: An array of objects, each containing `{value, label}`. -->

- **inputs**: 必須。配列｜オブジェクト。入力値。
  - 配列が指定された場合は、コンストラクタのオプションで指定された順序に合わせます。 
  - オブジェクトが指定された場合は、コンストラクタのオプションで指定されたキーと一致するキー/値のペアを指定します。 
- **callback(results)**: 必須。関数。`.predict()` の結果を処理する関数。 

**戻り値:**

- **Array**: 配列：`{value, label}`を含むオブジェクトの配列。

---

### nn.predictMultiple()

<!-- This method returns an array of arrays of predictions for the given input. -->
このメソッドは、与えられた入力に対する予測値の配列の配列を返します。

```javascript
nn.predictMultiple(inputs, callback);
```

<!-- **Parameters:**

- **inputs**: Required. Array of arrays | Array of objects.
  - If an array of arrays is given, then the input values of each child array should match the order that the data are specified in the `inputs` of the constructor options.
  - If an array of objects is given, then the input values of each child object should be given as a key/value pair. The keys must match the keys given in the inputs of the constructor options and/or the keys added when the data were added in `.addData()`.
- **callback**: Required. Function. A function to handle the results of `.classifyMultiple()`.

**Returns:**

- **Array**: An array of arrays, each containing objects with `{value, label}`. -->

**パラメータ:**

- **inputs**: 必須。配列の配列｜オブジェクトの配列。
  - 配列の配列が指定された場合、各子配列の入力値はコンストラクタのオプションの`inputs`で指定された順序と一致しなければなりません。
  - オブジェクトの配列が指定された場合、各子オブジェクトの入力値はキーと値のペアで指定されなければなりません。キーは、コンストラクタのオプションの入力で指定されたキー、および/または `.addData()` でデータが追加されたときに追加されたキーと一致しなければなりません。
- **callback**: 必須。関数。`.classifyMultiple()`の結果を処理する関数。

**戻り値:**

- **配列**: `{value, label}`のオブジェクトを含む配列の配列。

---

### nn.classify()

<!-- This method returns an array of classifications for the given input. -->
このメソッドは、指定された入力に対する分類の配列を返します。

```javascript
nn.classify(inputs, callback);
```

<!-- **Parameters:**

- **inputs**: Required. Array | Object. Input values.
  - If an array is given, match the order specified in the constructor options.
  - If an object is given, provide key/value pairs matching the keys specified in the constructor options.
- **callback(results)**: Required. Function. A function to handle the results of `.classify()`.

**Returns:**

- **Array**: An array of objects, each containing `{label, confidence}`. -->

**パラメータ:**

- **inputs**: 必須。配列 | オブジェクト。入力値。 
  - 配列が指定された場合は、コンストラクタのオプションで指定された順序に合わせる。 
  - オブジェクトが指定された場合は、コンストラクタのオプションで指定されたキーと一致するキー/値のペアを指定します。
- **callback(results)**: 必須。関数。`.classify()`の結果を処理する関数。

**戻り値:**

- **配列**: それぞれ `{label, confidence}`を含むオブジェクトの配列。

---

### nn.classifyMultiple()

<!-- This method returns an array of arrays of classifications for the given input. -->
このメソッドは、指定された入力に対する分類の配列の配列を返します。 

```javascript
nn.classifyMultiple(inputs, callback);
```

<!-- **Parameters:**

- **inputs**: Required. Array of arrays | Array of objects. Input values.
  - If an array of arrays is given, match the order specified in the constructor options.
  - If an array of objects is given, provide key/value pairs matching the keys specified in the constructor options.
- **callback(results)**: Required. Function. A function to handle the results of `.classifyMultiple()`.

**Returns:**

- **Array**: An array of arrays, each containing objects with `{label, confidence}`. -->

**パラメータ:**

- **inputs**: 必須。配列の配列｜オブジェクトの配列。入力値。
  - 配列の配列が指定された場合は、コンストラクタのオプションで指定された順序に合わせる。
  - オブジェクトの配列が指定された場合は、コンストラクタのオプションで指定されたキーと一致するキー/値のペアを指定します。 
- **callback(results)**: 必須。関数。`.classifyMultiple()`の結果を処理する関数。 

**戻り値:**

- **Array**: それぞれ `{label, confidence}`を持つオブジェクトを含む配列の配列。

---

### nn.saveData()

<!-- This method saves the added data to a JSON file. -->
このメソッドは、追加されたデータを JSON ファイルに保存します。

```javascript
nn.saveData(outputName, callback);
```

<!-- **Parameters:**

- **outputName**: オプション. 文字列. The name of the saved file. Default is `data_YYYY-MM-DD_mm-hh`.
- **callback**: オプション. Function. A callback function to be called after the data has been saved.

**Returns:**

- n/a: Downloads the data to a `.json` file. -->

**パラメータ:**

- **outputName**: オプション。文字列。保存されるファイルの名前。デフォルトは`data_YYYY-MM-DD_mm-hh`。
- **callback**: オプション。関数。データ保存後にコールされるコールバック関数。

**戻り値:**

- n/a: データを`.json`ファイルにダウンロードします。

---

### nn.loadData()

<!-- This method loads data to `neuralNetworkData.data.raw`. -->
このメソッドは、`neuralNetworkData.data.raw` にデータをロードします。 
```javascript
nn.loadData(filesOrPath, callback);
```

<!-- **Parameters:**

- **filesOrPath**: REQUIRED. 文字列 | InputFiles. A string path to a `.json` data object or InputFiles from html input `type="file"`. Must be structured for example as: `{"data": [ { xs:{input0:1, input1:2}, ys:{output0:"a"},  ...]}`
- **callback**: オプション. function. A callback that is called after the data has been loaded.

**Returns:**

- n/a: Sets `neuralNetworkData.data.raw` to the array specified in the incoming JSON file. -->

**パラメータ:**

- **filesOrPath**: 必須。文字列｜ 入力ファイル。 htmlのinput `type="file"` から `.json` データオブジェクトまたは 入力ファイル への文字列パス。 例えば、以下のような構造でなければならない: `{"data": [ { xs:{input0:1, input1:2}, ys:{output0:"a"},  ...]}`
- **callback**: オプション。 関数。 データがロードされた後に呼び出されるコールバック。

**戻り値:**

- n/a: `neuralNetworkData.data.raw`を、入力されたJSONファイルで指定された配列に設定します。 

---

### nn.save()

<!-- This method saves the trained model. -->
このメソッドは学習済みモデルを保存します。
```javascript
nn.save(outputName, callback);
```

<!-- **Parameters:**

- **outputName**: オプション. 文字列. The name of the saved file. Default is `model`.
- **callback**: オプション. Function. A callback function to be called after the model has been saved.

**Returns:**

- n/a: Downloads the model to a `.json` file and a `model.weights.bin` binary file. -->

**パラメータ:**

- **outputName**: オプション。 文字列。 保存されるファイルの名前。デフォルトは`model`。
- **callback**: オプション。関数。 モデルが保存された後に呼び出されるコールバック関数。

**戻り値:**

- n/a: モデルを`.json`ファイルと`model.weights.bin`バイナリファイルにダウンロードします。 

---

### nn.load()

<!-- This method loads a pre-trained model. -->
このメソッドは、事前に訓練されたモデルをロードします。 

```javascript
nn.load(filesOrPath, callback);
```

<!-- **Parameters:**

- **filesOrPath**: Required. 文字列 | InputFiles. The URL to the `model.json` file, or InputFiles from an HTML input element.
  - If a string path to the `model.json` data object is given, then the `model.json`, `model_meta.json` file and its accompanying `model.weights.bin` file will be loaded. Note that the names must match.
  - If InputFiles from html input `type="file"`. Then make sure to select ALL THREE of the `model.json`, `model_meta.json` and the `model.weights.bin` file together to upload otherwise the load will throw an error.
  - Method 1: Using a JSON object with paths to specific files:
    ```javascript
    const modelInfo = {
      model: "path/to/model.json",
      metadata: "path/to/model_meta.json",
      weights: "path/to/model.weights.bin",
    };
    nn.load(modelInfo, modelLoadedCallback);
    ```
  - Method 2: Specifying only the path to the `model.json`. Assumes the `model_meta.json` and `model.weights.bin` are in the same directory:
    ```javascript
    nn.load("path/to/model.json", modelLoadedCallback);
    ```
  - Method 3: Using `<input type="file" multiple>`:
- **callback**: オプション. Function. A callback function to be called after the model has been loaded. -->

**パラメータ:**

- **filesOrPath**: 必須。 文字列 | 入力ファイル `model.json`ファイルへのURL、またはHTML入力要素からの入力ファイル。 
  - `model.json`データオブジェクトへの文字列パスが与えられた場合、`model.json`、`model_meta.json`ファイル、およびそれに付随する`model.weights.bin`ファイルがロードされます。名前が一致していなければならないことに注意。
  - htmlのinput `type="file"`の入力ファイルの場合。この場合、`model.json`、`model_meta.json`、`model.weights.bin`の3つのファイルを一緒にアップロードするように選択してください。
  - メソッド 1: 特定のファイルへのパスを持つJSONオブジェクトを使用する:
    ```javascript
    const modelInfo = {
      model: "path/to/model.json",
      metadata: "path/to/model_meta.json",
      weights: "path/to/model.weights.bin",
    };
    nn.load(modelInfo, modelLoadedCallback);
    ```
  - メソッド 2: `model.json`へのパスのみを指定する。`model_meta.json`と`model.weights.bin`が同じディレクトリにあると仮定します:
    ```javascript
    nn.load("path/to/model.json", modelLoadedCallback);
    ```
  - メソッド 3: `<input type="file" multiple>`を使う:
- **callback**: オプション。関数。 モデルがロードされた後に呼び出されるコールバック関数。 

<!-- **Returns:**

- n/a: Loads the model to `nn.model`. -->
**戻り値:**

- n/a: モデルを`nn.model`にロードします。

---

### nn.mutate()

<!-- This method mutates the weights of a model. -->
このメソッドはモデルの重みを変更します。 

```javascript
nn.mutate(rate, mutateFunction);
```

<!-- **Parameters:** -->
**パラメータ:**

<!-- - **rate**: オプション. Number. The rate of mutation. Default is `0.1`. -->
<!-- - **mutateFunction**: オプション. Function. A function to mutate the weights. Default is a random Gaussian function. -->
- **rate**: オプション。数値。突然変異の割合。デフォルトは`0.1`。
- **mutateFunction**: オプション。関数。重みを変異させる関数。デフォルトはランダムなガウス関数。 

<!-- **Returns:** -->
**戻り値:**

<!-- - n/a: Mutates the weights of the model. -->
- n/a: モデルの重みを変更します。

<!-- ?> This method is created to build neuroevolution systems. If you are interested in neuroevolution, you can learn more about it with [Nature of Code Chapter 11](https://natureofcode.com/neuroevolution/). -->
?> この方法は neuroevolution ()システムを構築するために作られました。neuroevolution ()に興味があれば、[Nature of Code第11章](https://natureofcode.com/neuroevolution/)で詳しく学ぶことができます。

---

### nn.crossover()

<!-- This method creates a new neural network with crossover. -->
このメソッドはクロスオーバーで新しいニューラルネットワークを作成します。

```javascript
nn.crossover(other);
```

<!-- **Parameters:** -->
**パラメータ:**
<!-- - **other**: Required. Object. Another neural network object. -->
- **other**: 必須。オブジェクト。別のニューラルネットワークオブジェクト。

<!-- **Returns:** -->
**戻り値:**

<!-- - **Object**: A new neural network object with the weights of the two models crossed over. -->
- **Object**: 2つのモデルの重みを掛け合わせた新しいニューラルネットワークオブジェクト。 
<!-- ?> This method is created to build neuroevolution systems. If you are interested in neuroevolution, you can learn more about it with [Nature of Code Chapter 11](https://natureofcode.com/neuroevolution/). -->
?> この方法は neuroevolution ()システムを構築するために作られました。neuroevolution ()に興味があれば、[Nature of Code第11章](https://natureofcode.com/neuroevolution/)で詳しく学ぶことができます。


  