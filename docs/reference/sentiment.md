# Sentiment

<center>
  <img class="header-img" src="assets/header-sentiment.png" alt="Sentiment Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/kartini7/" target="_blank" title="kartini 1">kartini 1</a> | <a href='mailto:info@ml5js.org'>Contribute \CID{206}</a> </p>
</center>

## 概要

<!--
Sentiment is a model trained to predict the sentiment of any given text. For example, it can predict how positive or negative a review is with a value between 0 ("negative") and 1 ("positive").

The model is trained using IMDB reviews that have been truncated to a maximum of 200 words, and only the 20000 most used words in the reviews are used.
-->
センチメントは、任意のテキストの感情を予測するためにトレーニングされたモデルです。例えば、レビューがどれほどポジティブ、もしくはネガティブであるかを、0（否定的）から1（肯定的）の間の値によって予測できます。
このモデルは、最大200の語に切り詰められたIMDBレビューの使用によりトレーニングされ、レビューで最も使用される20000の語のみが使用されます。 

<!--
It provides the following functionalities:
-->
以下の機能を提供します： 

<!--
- **Sentiment Analysis**: The model can predict the sentiment of a given text.
-->
- **センチメント分析**: このモデルは、任意のテキストの感情を予測できます。 

<!--
## Quick Start
-->
## クイックスタート!

<!--
Run and explore a pre-built example! [This Sentiment example](https://editor.p5js.org/ml5/sketches/hopIvsCGL) predicts the sentiment of the given text.
-->
事前構築された例を実行し調べてみましょう。[このセンチメントのサンプル](https://editor.p5js.org/ml5/sketches/hopIvsCGL)は任意のテキストの感情を予測します。 

</br>

[DEMO](iframes/sentiment ":include :type=iframe width=100% height=550px")

<!--
## Examples
-->
## サンプル

<!--
- [Sentiment Analysis](https://editor.p5js.org/ml5/sketches/hopIvsCGL): Predict the sentiment of the given text.
-->
- [センチメント分析](https://editor.p5js.org/ml5/sketches/hopIvsCGL): 任意のテキストの感情を予測します。

<!--
## Step-by-Step Guide
-->
## 段階的なガイド

<!--
Now, let's together build the [Sentiment Analysis example](https://editor.p5js.org/ml5/sketches/hopIvsCGL) from scratch, and in the process, learn how to use the Sentiment model.
-->
では、ゼロから[センチメント分析の例](https://editor.p5js.org/ml5/sketches/hopIvsCGL)を一緒に構築し、その過程で、センチメントモデルの使用法を学びましょう。

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
Let's open the `sketch.js` file and define a variable to store the Sentiment model.
-->
`sketch.js`ファイルを開き、センチメントモデルを保存する変数を定義しましょう。 


```javascript
let sentiment;
```
<!--
Now, create a `preload` function and load the Sentiment model by calling the `ml5.sentiment(model, ?callback)` method. Using the `preload` function lets us make sure that the model is loaded correctly before the `setup` and `draw` functions are called.
-->
ここで、`preload` 関数を作成し、\UTF{202F}`ml5.sentiment(model, ?callback)`\UTF{202F}メソッドを呼び出してセンチメントモデルをロードします。\UTF{202F}`preload`関数を用いると、\UTF{202F}`setup`\UTF{202F}と`draw`関数が呼び出される前に、モデルが正しくロードされていることを確かめることができます。

<!--
Currently, the Sentiment model only supports the 'movieReviews' model, and we may support more models in the future.
-->
現在、センチメントモデルは "movieReviews" モデルのみをサポートしており、将来的にはより多くのモデルをサポートするでしょう。 


```javascript
function preload() {
  // Initialize the sentiment analysis model
  sentiment = ml5.sentiment("MovieReviews");
}
```

<!--
Since we are not going to draw anything on the canvas and will instead update the HTML elements directly to interact with the model, we can remove the canvas within the `setup` function.
-->
キャンバスはデフォルトで生成されますが、今回はキャンバスを必要としないので、`setup`関数内でキャンバスを削除し、モデルと対話するためにHTML要素をアップデートします。 

```javascript
function setup() {
  noCanvas();
}
```

<!--
### Set up UI for user interaction
-->
### ユーザーインタラクションのためのUI を設定する

<!--
To give the user some guidance on how to interact with the model, we can add a prompt message. Open the `index.html` file and add the prompt message within the `<body>` tag.
-->
モデルとの対話方法のガイダンスをユーザーに提供するために、プロンプトメッセージを追加することができます。`index.html`を開き、`\UTF{202F}<body>`タグ内にプロンプトメッセージを追加します。 

```html
<body>
  <h1>Sentiment Analysis Demo</h1>
  <p>
    This example uses model trained on movie reviews. This model scores the
    sentiment of text with a value between 0 ("negative") and 1 ("positive").
    The movie reviews were truncated to a maximum of 200 words and only the
    20,000 most common words in the reviews are used.
    <br />
    Press 'Enter' on your keyboard or 'Submit' to see score!
  </p>

  <script src="sketch.js"></script>
</body>
```

<!--
To allow the user to interact with the model, we need an input field for the user to provide the text to predict the sentiment of, a button to submit the text, and a paragraph element to display the sentiment prediction result. Let's define the variables to store these elements in the `sketch.js` file.
-->
ユーザーがモデルと対話できるようにするためには、感情を予測するテキストをユーザーが提供するための入力フィールド、テキストを送信するためのボタン、センチメント予測の結果を表示するための段落要素が必要です。これらの要素を`sketch.js`ファイルに保存するための変数を定義しましょう。 

 

```javascript
let inputBox;
let submitBtn;
let sentimentResult;
```

<!--
Let's tackle these one by one! We can start with the input field to receive the text input from the user. In `setup`, use the `createInput` function to create an input field in the DOM, and set the default text to "Today is the happiest day and is full of rainbows!".
-->
これらに一つずつ取り組んでいきましょう。ユーザーからテキストを受け取るための入力フィールドから始めましょう。`setup`では、DOMに入力フィールドを作成するために`createInput`関数を使用し、"Today is the happiest day and is full of rainbows!"とデフォルトテキストを設定します。


```javascript
function setup() {
  ...
  // Set up the DOM elements
  inputBox = createInput("Today is the happiest day and is full of rainbows!");
```

<!--
Set the size of the input box to 75 pixels.
-->
入力ボックスのサイズを75ピクセルに設定します。

```javascript
inputBox.attribute("size", "75");
```

<!--
Now, we can create a button that the user can click to predict the sentiment of the text. We can use the `createButton` function to create a button in the DOM, and set the button text to "submit".
-->
これで、テキストの感情を予測するためにユーザーがクリックできるボタンが作成できます。`createButton`関数を使用してDOMにボタンを作成し、ボタンのテキストを"submit"に設定します。

```javascript
submitBtn = createButton("submit");
```

<!--
Lastly, we can add a paragraph element to display the sentiment prediction result.
-->
最後に、センチメント予測の結果を表示するための段落要素を追加できます。 


```javascript
  sentimentResult = createP("Sentiment confidence:");
}
```

<!--
### Predict sentiment with the model
-->
### モデルを用いたセンチメント予測

<!--
Now that we have set up the UI, we can predict the sentiment of the text input by the user. Let's define a function `getSentiment` that will be called when the user clicks the submit button or presses the enter key.
It will get the values from the user input, and store it in a variable `text`.
-->
UIを設定したので、ユーザーにより入力されたテキストの感情を予測できます。ユーザーが送信ボタンをクリックするか、エンターキーを押した時に呼び出される`getSentiment`関数を定義しましょう。
ユーザーの入力から値を取得し、`text`変数に保存します。 

```javascript
function getSentiment() {
  // Use the value of the input box
  let text = inputBox.value();
```

<!--
Make the prediction using the `predict` method of the `sentiment` object. Here, we pass two parameters: the input text and a customized callback function `gotResult`.
-->
`sentiment`オブジェクトの`predict`メソッドを使用して予測してください。ここでは、入力テキストとカスタマイズされたコールバック関数である`gotResult`の二つのパラメータを渡します。

```javascript
  // Start making the prediction
  sentiment.predict(text, gotResult);
}
```

<!--
The `gotResult` function is a callback function that will be called when the `predict` method predicts the text's sentiment. Once the sentiment is predicted, the output `prediction` will be passed to `gotResult`, and then display the sentiment confidence in the paragraph element `sentimentResult`.
-->
`gotResult`関数は、`predict`メソッドがテキストの感情を予測する時に呼び出されるコールバック関数です。一度センチメントが予測されると、`prediction`の出力が`gotResult`に渡され、段落要素の`sentimentResult`にセンチメントの信頼度が表示されます。 


```javascript
function gotResult(prediction) {
  // Display sentiment result via the DOM
  sentimentResult.html("Sentiment confidence: " + prediction.confidence);
}
```
<!--
The only thing left is to call the `getSentiment` function when the user clicks the submit button or presses the 'enter' key.

To do this, let's first go back to the `setup` function. We can use the `mousePressed` function of the `submitBtn` object, which will call a function when the mouse is pressed over the element.
-->
ユーザーが送信ボタンをクリックするか、「Enter」キーを押した時に`getSentiment`を呼び出すことだけが残ります。これを行うために、`setup`関数にまず戻りましょう。`submitBtn`オブジェクトの`mousePressed`関数を使用すると、要素上でマウスが押された時に関数を呼び出します。

```javascript
function setup() {
  ...
  sentimentResult = createP("Sentiment confidence:");

  // Start predicting when the submit button is pressed
  submitBtn.mousePressed(getSentiment);
}
```

<!--
Now, we'll create a `keyPressed` function and call the `getSentiment` function when the user presses the 'enter' key.
-->
ここで、`keyPressed`関数を作成し、ユーザーが「Enter」キーを押した時に`getSentiment`関数を呼び出します。

```javascript
// Start predicting when the 'Enter' key is pressed
function keyPressed() {
  if (keyCode == ENTER) {
    getSentiment();
  }
}
```

<!--
### Run your sketch
-->
### スケッチを実行する

<!--
That's it! You have successfully built a Sentiment Analysis model that predicts the sentiment of the given text. Press the <img class="inline-img" src="assets/facemesh-arrow-forward.png" alt="run button icon" aria-hidden="true"> `run` button to see the code in action. You can also find the [complete code](https://editor.p5js.org/ml5/sketches/hopIvsCGL) in the p5.js web editor.
-->
できましたね！任意のテキストの感情を予測するセンチメント分析モデルの構築に成功しました！コードの動作を見るためには実行ボタンを押してください。p5.jsのwebエディターで[完全なコード](https://editor.p5js.org/ml5/sketches/hopIvsCGL)を確認することもできます。  

<!--
?> If you have any questions or spot something unclear in this step-by-step code guide, we'd love to hear from you! Join us on [Discord](https://discord.com/invite/3CVauZMSt7) and let us know how we can make it better.
-->
?> この段階的なコードガイドで質問や不明点がございましたら、ぜひご連絡ください。[Discord](https://discord.com/invite/3CVauZMSt7)に参加して、改善点をお知らせください。

<!--
## Properties
-->
## プロパティ


### sentiment.ready

- **Description**
  - Boolean value that specifies if the model has loaded.
- **Type**
  - Boolean

---

### sentiment.model

- **Description**
  - The TensorFlow.js model used for sentiment analysis.
- **Type**
  - tf.LayersModel

---

### sentiment.indexFrom

- **Description**
  - The starting index for words in the model's vocabulary.
- **Type**
  - Number

---

### sentiment.maxLen

- **Description**
  - The maximum length of sequences that the model can process.
- **Type**
  - Number

---

### sentiment.wordIndex

- **Description**
  - An object mapping words to their corresponding indices in the model's vocabulary.
- **Type**
  - Object

---

### sentiment.vocabularySize

- **Description**
  - The size of the vocabulary that the model was trained on.
- **Type**
  - Number

<!--
## Methods
-->
## メソッド

### ml5.sentiment()

<!--
This method is used to load the sentiment model and store it in a variable. The ? means the argument is optional!
-->
このメソッドは、感情モデルをロードして変数に保存するために使用されます。? は、引数がオプションであることを意味します。

```js
let sentiment = ml5.sentiment(model, ?callback);
```

<!--
#### Parameters
-->
#### パラメータ

<!--
- **model**: REQUIRED. Defaults to 'movieReviews'. You can also use a path to a `manifest.json` file via a relative or absolute path.
- **callback(sentiment, error)**: Optional. A callback function that is called once the model has loaded. If no callback is provided, it will return a promise that will be resolved once the model has loaded.
-->
- **モデル**: 必須.デフォルトは 'movieReviews' です。相対パスまたは絶対パスを使用して`manifest.json`ファイルへのパスも指定できます。
- **callback(sentiment, error)**: オプション。モデルの読み込みが完了した際に呼び出されるコールバック関数です。コールバックが提供されていない場合、モデルが読み込まれると解決されるpromiseが返されます。

---

### sentiment.predict()

<!--
This method is used to predict the sentiment of a given text.
-->
このメソッドは、任意のテキストの感情を予測するために使用されます。

```js
sentiment.predict(text);
```

<!--
**Parameters:**
-->
**パラメータ:**
<!--
- **text**: Required. 
  - String: A string of text to predict. 
-->
- **テキスト**: 必須. 
  - 文字列: 予測するテキストの文字列. 

<!--
**Return:**
-->
**返り値:**

<!--
- **Object**: Scores the sentiment of given text with a value between 0 ("negative") and 1 ("positive"). See below for an example output:
-->
- **オブジェクト**: 指定されたテキストの感情を 0 (「否定的」) から 1 (「肯定的」) の間の値でスコア付けします。出力例については以下を参照してください。

  ```javascript
  {
    confidence: 0.9999948740005493;
  }
  ```