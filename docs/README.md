
# Getting Started 

<center>
  <img class="header-img" src="assets/header-getting-started.png" alt="Getting Started Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/ifkirianto.if" target="_blank" title="Iki">Iki</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

<!-- 
Welcome! We're going to walk through how to start using ml5.js by creating a simple image classification program.

This page will cover how to:

1. Load a pre-trained ml5.js image classification model
2. Load an image for the model to identify the object in the image
3. Get the results from the model and display them on the canvas

We will using a p5.js sketch running on the [p5.js web editor](https://editor.p5js.org/). To get started, open up the p5.js web editor and create an empty project. Be sure to sign up or log in to your account so that you are able to upload files! This will be necessary later on as we upload images. 
-->
ようこそ！
ml5.jsを使ってシンプルな画像分類プログラムを作ってみましょう

このページでは以下の内容が含まれています．

1，	学習済みのml5.jsの画像分類モデルを読み込む
2，	画像内のオブジェクトを認識するために，モデルに画像を読み込む
3，	モデルから結果を取得し，キャンバスへ結果を表示する．

私たちはp5.jsスケッチの実行にp5.jsウェブエディターを使います．始めるにはp5.jsウェブエディターを開き新規のスケッチを作成します.ファイルのアップロードが出来るようにするために必ずサインアップかログインをしてください！後ほど画像ファイルをアップロードするために必要になります．


<!-- 
?> You can find the full code for this tutorial at [imageClassifier single image example code](https://editor.p5js.org/ml5/sketches/pjPr6XmPY). Press the run button to see the code in action.
 -->

?> あなたは１つの画像から画像分類をするサンプルコードを[ここから](https://editor.p5js.org/ml5/sketches/pjPr6XmPY)見つける事ができます．実行ボタンを押してプログラムの振る舞いを見てみましょう

## ml5jsのセットアップ {docsify-ignore}

<!-- 
## Set up ml5.js {docsify-ignore} 
-->

<!--
 Once you have the p5.js web editor open, unfold the project directory by clicking the arrow `>` at the top left corner.
 -->

まず，p5jsウェブエディターを開いたら左上隅の矢印 `>` をクリックしてプロジェクトディレクトリを開きます．


<!-- TODO: photoshop image so that all have 800 px width before styling -->
<center>
    <img alt="screenshot of sketch files on the p5 web editor interface" width="800" src="assets/gettingstarted-sketch-folder-alpha.png">
</center>

<!--
 Now, let's switch to the `index.html` file and copy and paste the following CDN link inside the `<head>` tag.
-->

次に，`index.html` ファイルを選択して `<head>` タグ内に以下のCDNリンクをコピーします．

```html
<script src="https://unpkg.com/ml5@1/dist/ml5.min.js"></script>
```

<center>
    <img alt="screenshot of importing ml5 library in index.html file" width="800" src="assets/gettingstarted-import-lib-alpha.png">
</center>

<!--
 ## Load pretrained ml5.js model {docsify-ignore}
-->

## 学習済みのml5.jsモデルを読み込む {docsify-ignore}

<!--
 Use the project directory to switch back to the `sketch.js` file. We will define a variable called `classifier` to hold the image classifier model.
-->

プロジェクトディレクトリを使用して `sketch.js` ファイルに戻ります．画像分類モデルを保持するために `classifier` という変数を定義します．

```js
let classifier;
```

<!--
 Next, add a `preload()` function to load the image classification model. In this example, we are using the MobileNet model. 
-->

次に画像分類モデルを読み込むための `preload()` 関数を追加します．このサンプルではMobileNetモデルを使っています．

```js
function preload() {
  classifier = ml5.imageClassifier("MobileNet");
}
```

<!--
 ?> If you are not familiar with terms like `pretrained model`, `classification`, `classifier`, `preload function`, or `MobileNet` and would like to learn more about them, check out our [ml5 Glossary](/learn/ml5-glossary) for a quick intro.
-->

?> もし．事前学習済みモデル(`pretrained model`)や分類（`classification`），分類器（`classifier`）preload()関数（p`preload function`），`MobileNet`に馴染みがなく，もっと詳しく知りたい場合は[ml5 Glossary](/learn/ml5-glossary)を確認してみてください

<!--
 ## Load an image for the model to identify {docsify-ignore} 
-->
## 認識のための画像を読み込む {docsify-ignore}

<!--
 Let's unfold the project directory again by clicking the arrow `>` at the top left corner of the p5.js editor.
-->

もう一度矢印 `>` をクリックしてプロジェクトファイルを展開してみましょう

<center>
    <img alt="screenshot of sketch files on the p5 web editor interface" width="800" src="assets/gettingstarted-sketch-folder-alpha.png">
</center>

<!--
 Select the `+` to create a new folder called `images`. 
-->

`+`を選択して`images`というフォルダを作成します

<center>
    <img alt="screenshot of creating images folder" width="800" src="assets/gettingstarted-create_folder_alpha.png">
</center>

<!--
 To upload files to the folder, choose the `images` folder in the project directory and upload an image using the drop-down menu. For this example, we are uploading an image of a bird called `bird.png`. Make sure you are logged in to see this option. 
-->

フォルダーにアップデートするには，プロジェクトディレクトリの `イメージフォルダ`を選びドロップダウンメニューから画像をアップロードします．この例では， `bird.png` という鳥の画像をアップロードします．この設定を表示するにはログインしていることを確認してください．

<center>
    <img alt="screenshot of uploading file to p5 web editor" width="800" src="assets/gettingstarted-upload-file-alpha.png">
</center>

<!--
 Once the image is uploaded, go back to the `sketch.js` file and define a variable called `img` to hold the image you want to classify. 
-->

次に，画像をアップロードします． `sketch.js` に戻り，画像を保持するための `img` という変数を定義します．

```js
let img;
```

<!-- 
Within the `preload()` function, load the image using the `loadImage()` function. 
-->

`preload()`関数で`loadImage()`関数を使用して画像を読み込みます．

```js
function preload() {
  classifier = ml5.imageClassifier("MobileNet");
  img = loadImage("images/bird.png");
}
```

<!-- ## Make predictions with the model {docsify-ignore} -->
## モデルでの予測を行う {docsify-ignore}

In the `setup()` function, we will call the `classify()` function on the `classifier` object to classify the image. The `classify()` function takes two parameters: the image you want to classify and a callback function called `gotResult`.

この`setup()`関数では，`classify()`という`classifier`オブジェクトを呼び出し，画像を分類します．
`classify()`関数は２つの引数を持ちます．:分類したい画像imgとコールバック関数の`gotResult` を呼びます


```js
function setup() {
  createCanvas(400, 400);
  classifier.classify(img, gotResult);
}
```

<!--
 Now, let's define the `gotResult()` function. The callback function `gotResult()` is a function that will be called when the `classify()` function finishes classifying the image.
-->

次に，`gotResult()`関数を定義していきましょう．このコールバック関数`gotResult()` は`classify()`関数が画像分類を終えたときに呼び出されます．

```js
function gotResult(results) {
  console.log(results);
}
```

<!--
 ?> If you are not familiar with the concept of `callback` and would like to learn more about it, check out our [ml5 Glossary](/learn/ml5-glossary) for more information.
 -->

?> もし，コールバック（`callback`）という概念に馴染みがなく，もっと詳しく知りたい方は[ml5 Glossary](/learn/ml5-glossary)にもっと詳しく乗っています．

## Display the results on the canvas {docsify-ignore}
## 結果をキャンバスに表示する． {docsify-ignore}

<!--
 As we discussed above, the `gotResult()` function will be called when the `classify()` function finishes classifying the image. A variable `results` that contains the results of the classification will be passed along to `gotResult()`. Let's take a look at the `results` that is received by the `gotResult()` function.
-->

これまでに説明したように，`classify()`関数で画像の分類が終了すると`gotResult()`関数が呼び出されます．分類結果を格納した変数`results`がgotResult()関数に渡されます．`gotResult()`関数が受け取った`results`の中身を見てみましょう

```js
[
  {
    label: "robin, American robin, Turdus migratorius",
    confidence: 0.9026526212692261,
  },
  {
    label: "worm fence, snake fence, snake-rail fence, Virginia fence",
    confidence: 0.0029119430109858513,
  },
  {
    label: "brambling, Fringilla montifringilla",
    confidence: 0.0015617000171914697,
  },
];
```

<!--
 The `results` is an array of objects ordered by confidence. The object at index 0 has the highest confidence. By default, ml5.js image classifier MobileNet model returns the top 3 labels with their confidence scores. In this example, we are interested in only the top result that has the highest confidence, which is the label that has the highest probability of being correct. 
-->

`results`は信頼度順に並べられたオブジェクトの配列です．オブジェクトの添字0番はもっとも信頼度が高いです．デフォルトでは，ml5.jsの画像分類モデルであるMobileNetモデルは上位３つのラベルと信頼度スコアを返します．この例では、最も信頼度が高い結果、つまり正しい可能性が最も高いラベルのみに注目しています．



<!--
 To get this, we are going to define two variables `label` and `confidence` to store the label and confidence of the top 1 result.
-->

これを得るために，variables `label` と `confidence`の２つの変数を定義し上位1位の結果ラベルと信頼度を格納します．


```js
let label = "";
let confidence = "";
```

<!--
 In the `gotResult()` function, let's display the label and confidence of the top 1 result on the canvas using the `text()` function.
 -->

`gotResult()`関数でラベルと信頼度の1位を`text()`関数を使って出力してキャンバスに表示してみましょう．

```js
function gotResult(results) {
  console.log(results);

  fill(255);
  stroke(0);
  textSize(18);
  label = "Label: " + results[0].label;
  confidence = "Confidence: " + nf(results[0].confidence, 0, 2);
  text(label, 10, 360);
  text(confidence, 10, 380);
}
```

Lastly, render the image to the canvas using the `image()` function.

最後に`image()`関数を使ってキャンバスに画像を表示させます

```js
function setup() {
  createCanvas(400, 400);
  classifier.classify(img, gotResult);
  image(img, 0, 0);
}
```

<!--
 ?> If you are not familiar with terms like `label`, `confidence` and would like to learn more about them, check out our [ml5 Glossary](/learn/ml5-glossary) for a quick intro. \
 -->

?> もし，ラベル（`label`）や信頼度（`confidence`）などの用語に馴染みがなく，もっと詳しく知りたい方は[ml5 Glossary](/learn/ml5-glossary)をご覧ください．


<!-- ## Run your sketch {docsify-ignore} -->
## スケッチを実行する {docsify-ignore}

<!--
 Now, you are ready to see the results! Run your sketch and see if the model can make predictions and provide meaningful outputs. Press the run button on the top left corner of the editor.
-->

これで，結果を見る準備ができました！スケッチを実行して，モデルが予測と意味のある出力ができるかみてください．エディタの左上の実行ボタンを押してください．

<!--
 You should get something like this: 
-->

このようなものが出力されるはずです:

<center>
    <img alt="screenshot of running a sketch" width=`800` src="assets/gettingstarted-run-sketch-alpha.png">
</center>

## And voilà! {docsify-ignore}
## ジャジャーン！！{docsify-ignore}

<!-- 
You've just made a simple machine learning powered program that: 
-->

簡単な機械学習のプログラムが出来上がりました．これには

<!-- 
1. takes an image,
2. classifies the content of that image,
3. and displays the results all in your web browser! 
-->
  1. 画像を読み込む
  1. 画像の内容を分類する
  2. そして，結果をWebブラウザに表示する！

<!--
 Not all of our examples are structured exactly like this, but this provides a taste into how ml5.js is trying to make machine learning more approachable. You can try using different images and seeing what kinds of things get returned. 
-->

私たちのすべてのサンプルがこのように構成されているわけではありませんが，ml5.jsが機械学習をより身近なものにしようとしていることを知る事ができます．ぜひ，さまざまな画像を試してみて，どのような結果が返ってくるか試してみてください

<br/>

<!--
 Some guiding questions you might start to think about are 
-->

いくつか考え始めるためのガイドとしての質問は以下の通りです．

<!-- 
1. Do you notice that MobileNet is better at classifying some animals over others? Why do you think that is?
2. Does the top result always accurately describe the image? 
-->

3. MobileNetは，特定の動物を他の動物よりもうまく分類していることに気づきましたか？それはなぜだと思いますか？
4. 最上位の結果は常に画像を正確に説明していますか？


<!-- ## What next? {docsify-ignore} -->

## 次にすることは？ {docsify-ignore}


Now that you've built your first ml5.js project, take a look at other models and explore how you might use ml5.js for ML-based projects! Check out the [Next Steps](/welcome/next-steps) page to learn more.

これまでに，最初のml5.jsのプロジェクトを構築しました．他のモデルも見てみて,ml5.jsに使った機械学習ベースのプロジェクトをどのように活用できるか探ってみましょう！[Next Steps](/welcome/next-steps)のページを見て，さらに学んでいきましょう．

<br>
