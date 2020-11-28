これは、このサイトで紹介されている AR を Angular に移植する手順です。

`【AR.js入門】簡単にWebARで遊んでみた【A-Frame使うよ】`
https://qiita.com/sakaryu/items/769a2a538baf7e4ee1c7



## 手順1.Angularプロジェクトを新規作成する

### 以下のコマンドをコマンドプロンプトに入力する

```
ng new プロジェクト名
```
プロジェクト名の部分には任意の文字

![](/img/001.png)

### 選択肢は以下のように入力した

``` 
? Would you like to add Angular routing? (y/N)  N
```

```
? Which stylesheet format would you like to use?
  CSS
> SCSS   [ https://sass-lang.com/documentation/syntax#scss                ]
  Sass   [ https://sass-lang.com/documentation/syntax#the-indented-syntax ]
  Less   [ http://lesscss.org                                             ]
  Stylus [ http://stylus-lang.com                                         ]                                            
```

### インストールが終了するとこのような画面がでるので、コマンドプロンプトを終了する

![](/img/002.png)


## 手順2.AR を表示するための変更

### フォルダ `src\assets` に モデルファイルをコピーする

![](/img/006.png)


### ファイル `src\index.html` を変更する

```html
<!doctype html>
<html lang="en">
<!-- A-Frame ライブラリの読み込み -->
<script src="https://aframe.io/releases/0.8.2/aframe.min.js"></script>
<!-- AR.js ライブラリの読み込み -->
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/1.5.0/aframe/build/aframe-ar.js"></script>
<head>
  <meta charset="utf-8">
  <title>DobokuAR</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body style='margin : 0px; overflow: hidden;'>
<a-scene embedded arjs="debugUIEnabled:false;trackingMethod:best;" vr-mode-ui="enabled: false">
  <a-assets>
    <a-asset-item id="santa-obj" src="./assets/model_obj/santa/santa.obj"></a-asset-item>
    <a-asset-item id="santa-mtl" src="./assets/model_obj/santa/santa.mtl"></a-asset-item>
  </a-assets>
  <a-marker preset="hiro">
    <a-obj-model id="santa" src="#santa-obj" mtl="#santa-mtl" position="0 0 0" scale="0.5 0.5 0.5" rotation="0 0 0">
    </a-obj-model>
    <a-text value="Merry X'mas!!!" position="0 1.3 0" align="center"></a-text>
  </a-marker>
  <a-entity camera></a-entity>
</a-scene>
  <app-root></app-root>
</body>
</html>
```

### ファイル `src\app\app.component.html` の内容を全て削除する

```html

```


## 手順3. 実行する

### 始めて実行する場合はターミナルに次のコマンドを入力し実行する

> npm install

![](/img/005.png)

### ターミナルに次のコマンドを入力し実行する

> npm start

`: Compiled successfully.`というコメントがでたら

![](/img/006.png)

ブラウザで `http://localhost:4200/` を開く

![](/img/008.gif)


## 手順4.GitHub Pages にアップロード（公開）するための設定

### モジュールとプロジェクトに追加インストールする

ターミナルに次のコマンドを入力し実行する

>npm i angular-cli-ghpages

![](/img/010.png)



### ファイル `angular.json` の `outputPath` を変更する

```
"outputPath": "dist/プロジェクト名",
↓↓↓↓↓
"outputPath": "dist",
```

![](/img/003.png)


### ファイル `package.json` の `build` を変更する

```
"build": "ng build",
↓↓↓↓↓
"build": "ng build --prod --base-href \"https://DoboPro.github.io/AR/\" && angular-cli-ghpages",

```

![](/img/004.png)

### 公開する

ターミナルに次のコマンドを入力し実行する

> npm run build

ここで、確認できる
https://DoboPro.github.io/AR