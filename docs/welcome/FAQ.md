# FAQ

<center>
  <img class="header-img" src="assets/header-faq.png" alt="Frequently Asked Question Header Image" >
  <p class="img-credit"> Image Credit: <a href="https://thenounproject.com/creator/purpleiconn/" target="_blank" title="Purple iconn">Purple iconn</a> | <a href='mailto:info@ml5js.org'>Contribute ♥️</a> </p>
</center>

<!-- 
## What happened to older ml5.js releases?
We noticed that many people have experienced issues with the library recently, seeing errors such as *"... is not a function"*. <img class="inline-img" src="assets/faq-cry.png" alt="tip icon" aria-hidden="true"> This is most likely due to code that was written for the library prior to the recent 1.0 release. The following should help you resolve any errors! <img class="inline-img" src="assets/faq-dizzy.png" alt="tip icon" aria-hidden="true"> <img class="inline-img" src="assets/faq-purple-heart.png" alt="tip icon" aria-hidden="true"> 
-->


## 以前リリースされていたml5.jsはどうなったのですか？
最近，ライブラリに関連して多くの人が「... is not a function」というエラーを目にしていることに気づきました．<img class="inline-img" src="assets/faq-cry.png" alt="tip icon" aria-hidden="true">これはおそらく，最近リリースされた1.0以前に書かれたコードが原因です．以下の情報がエラー解決の助けになるはずです！<img class="inline-img" src="assets/faq-dizzy.png" alt="tip icon" aria-hidden="true"> <img class="inline-img" src="assets/faq-purple-heart.png" alt="tip icon" aria-hidden="true">


<!-- 
### Quick Fix!
In the ml5 library's script tag, change latest to 0.12.2. If you are using p5.js, you can find the script tag in the index.html file of your p5 sketch.
-->

### 応急措置！
ml5ライブラリ内のスクリプトタグでlatestを0.12.2に変更する.
P5.jsを使用している場合，p5スケッチのindex.htmlファイル内にスクリプトタグがあります．


<!-- 
Change this: 
-->
ここを変更します:

```html
<script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
```

<!--
to this:
-->
このように変更します:

```html
<script src="https://unpkg.com/ml5@0.12.2/dist/ml5.min.js"></script>
```

<!-- Hope this works! <img class="inline-img" src="assets/faq-crossed-fingers.png" alt="tip icon" aria-hidden="true"> -->

これで動くはずです！<img class="inline-img" src="assets/faq-crossed-fingers.png" alt="tip icon" aria-hidden="true">

<!-- ### Why are there errors?
We recently released a new version of the library, updating from version `0.12.2` to `1.0.1` (yay!!!). The library was re-designed be even friendlier, and included several breaking changes. Some functions from the previous version (`0.12.2`) no longer exist in `1.0.1`. For example, `poseNet.on("pose", gotPose)` has been removed and changed to `bodyPose.detectStart(video, gotPose)`. -->

### なぜエラーが発生するの？
最近新しいライブラリのバージョンを`0.12.2`から`1.0.1`にアップデートしました．（イエイ！！！）．ライブラリを使いやすく再設計しましたが，いくつか重大な変更が含まれていました．以前のバージョン(`0.12.2`)で存在していたいくつかの関数は`1.0.1`では存在しません．例えば，`poseNet.on(“pose”,gotPose)`は削除され`bodyPose.detectStart(video, gotPose)`に変更されました．


<!-- The `ml5@latest` tag automatically uses the latest version of the library, which is version `1.0.1`. If you are on version `1.0.1` and attempt to call a function that has been removed, you will likely see the *"... is not a function"* error. By specifying `ml5@0.12.2` in the script tag, you can continue using the previous version of the library and call the now deprecated functions. -->

`ml5@latest`タグは自動的に最新バージョン（現在は`1.0.1`）を使用します．`1.0.1`で削除された関数を呼び出そうとすると「... is not a function」とエラーが表示される可能性があります．スクリプトタグで`ml5@0.12.2`を指定することで，以前のバージョンを引き続き使用し，削除された関数を呼び出すことができます．

<!--
 Since we have passed the `1.0.0` landmark, we will be following semantic versioning for future releases. Going forward, we recommend specifying a major version number in the script tag, such as `ml5@1`. Using `ml5@latest` might cause issues if and when there are additional breaking changes.
-->

`1.0.0`のバージョンを超えたため私たちはこれから，セマンティックバージョニングにしたがってリリースしていきます．今後は，`ml5@1`のように，スクリプトタグでメジャーバージョンを指定することをおすすめします．`ml5@latest`を使用すると将来さらに大幅な変更が加わった際，問題が発生する場合があります．

<!-- 
### Can I still access the older releases of the ml5.js, website and documentation?
We will still host version `0.12` of the library, however, it will no longer receive feature updates. You can still use the older versions of the library by specifying `ml5@0.12.2` (or earlier versions) in the `script` tag, just as what was done in the [Quick Fix](/welcome/faq?id=quick-fix) above.

The [archived website](https://archive.ml5js.org/) and [documentation](https://archive-docs.ml5js.org/) cover materials for versions `0.12` and earlier. 

We recommend giving the new library a try! The new reference document is a great place to start as well as a collection of example sketches showcasing the models and functions! 
-->

### 公開されていたml.5jsサイトやドキュメントにまだアクセスできますか？
ライブラリのバージョン`0.12`をこれからもホストします．しかし，新たな機能のアップデートは行なっていきません．上記の[応急処置](/welcome/faq?id=quick-fix)のように`script`タグで`ml5@0.12.2`（もしくはそれ以前のバージョン）を指定することで古いバージョンのライブラリも使うことができます．
[アーカイブされたウェブサイト](https://archive.ml5js.org/)と[ドキュメント](https://archive-docs.ml5js.org/)には，`0.12`以前の資料が含まれています．
新しいライブラリを使ってみることをお勧めします！新たなリファレンスは始めるにはとてもいい場所であり，サンプルスケッチではモデルと関数を紹介しています！

<!-- ### ml5.js 0.12.2 models and functions -->

###　ml5.js 0.12.2のモデルと関数

<!-- #### Updated new models! -->

<!-- 
- FeatureExtractor - coming back soon! (use 0.12.2 for now)
- ObjectDetection - coming back soon! (use 0.12.2 for now)
- PoseNet - Updated! (now BodyPose)
- BodyPix - Updated! (now BodySegmentation)
- HandPose - Updated! Still HandPose!
- FaceMesh - Updated! Still FaceMesh!
- FaceApi - Deprecated, use FaceMesh instead!
- UNet - Deprecated, use BodySegmentation instead!
- Image Classification - the same!
- Sound Classification - the same!
- Sentiment Analysis - the same!
- Neural Network – mostly the same, updates for neuroevolution!

#### Deprecated, use 0.12.2
- KNNClassifer - coming soon?
- kmeans - coming soon?
- StyleTransfer
- pix2pix
- CVAE
- DCGan
- SketchRNN
- PitchDetection
- CharRNN
- Word2Vec
-->

####　アップデートした新しいモデル！
- FeatureExtractor - 近日再登場！ ( 現在は0.12.2 使用)
- ObjectDetection - 近日再登場！ ( 現在は0.12.2 使用)
- PoseNet - Updated! (現在は BodyPose)
- BodyPix - Updated! (現在は BodySegmentation)
- HandPose - 更新！ 引き続き HandPose!
- FaceMesh - 更新！　引き続き FaceMesh!
- FaceApi - 廃止, FaceMesh を使用！
- UNet - 廃止, BodySegmentation を使用！
- Image Classification - 変更なし！!
- Sound Classification - 変更なし！!
- Sentiment Analysis - 変更なし！!
- Neural Network – ほとんど変更なし, ニューラルエボリューションの更新あり！
#### 廃止されました．0.12.2を使ってください
- KNNClassifer - 近日公開?
- kmeans - 近日公開?
- StyleTransfer
- pix2pix
- CVAE
- DCGan
- SketchRNN
- PitchDetection
- CharRNN
- Word2Vec

<!-- 
## Can I always use ml5.js in the p5.js web editor? 
-->

## Ml5.jsをp5.js web editorでいつでも使えますか？

<!-- Mostly! -->
ほとんどは！

<!--
 Some of the ml5.js sketches don't currently work in the [p5.js web editor](https://editor.p5js.org/). This is due to how the editor handles data files and network communication regarding making requests to external data, such as the large model files ml5.js uses.

There are lots of developments in the p5.js web editor as well as in ml5.js to make sure these environments all play nicely together. If something doesn't work in the web editor, the best thing to do is to try and run things locally if possible.
-->

いくつかのml5.jsスケッチは現在[p5.js web editor](https://editor.p5js.org/)で動きません．これはエディタがデータファイルやネットワーク通信をどのように処理するかに関連しており，ml5.jsが使用する大きなモデルファイルに対するリクエストに影響しています．
p5.jsウェブエディタとml5.jsの朗報でこれらの環境がうまく連携するように多くの開発が勧められています．ウェブエディタで動作しない場合，可能ならばローカルで試すことをお勧めします．


<!-- ## Can I use ml5.js with node.js? -->

##　Ml5.jsをnode.jsで使えますか？

<!--
Not at the moment.

ml5.js uses TensorFlow.js, which uses the browser's GPU to run all the calculations. As a result, all of the ml5.js functionalities are based around using the browser GPU. We hope to have ml5.js run in node.js sometime in the near future (especially now that [node.js supports TensorFlow.js](https://www.tensorflow.org/js/guide/nodejs)), but the current ml5.js setup does not support node.js.

For more discussion about node.js and ml5.js, visit this [issue thread](https://github.com/ml5js/ml5-library/issues/377).
-->

現時点ではできません．
ml5.jsはTensorFlow.jsを使用しており，ブラウザでGPUを使った全ての計算をしています．その結果，全てのml5.jsの全機能はブラウザーのGPUを基盤として使用しています．近い将来，node.jsでml5.jsを使用することを目指しています（特に，現在 [node.js は TensorFlow.jsをサポートしているため](https://www.tensorflow.org/js/guide/nodejs))）が．現在のml5.jsの設定ではnode.jsをサポートしていません．
Node.jsとml5.jsに関するさらなる議論については[こちら](https://github.com/ml5js/ml5-library/issues/377)のスレッドをご覧ください．


<br>
