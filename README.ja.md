# kenall-js

![](https://github.com/KEN-ALL/kenall-js/workflows/CI/badge.svg)

kenall-js は日本の郵便番号・住所検索APIサービス「[ケンオール](https://kenall.jp/)」のクライアントライブラリです。

## 使い方

kenall-jsはブラウザでそのまま利用可能なスタンドアロンのJavaScriptバンドルとしても、Node.jsのモジュールとしても利用することができます。

### ブラウザで使う場合

スクリプトを利用するHTMLファイルに

```html
<script type="text/javascript" src="https://js.kenall.jp/2021-02-01/kenall.js"></script>
```

を記載すると、(以降に読み込まれた`<script>`タグの中で) `window`オブジェクトに`kenall`オブジェクトが追加され、`kenall`オブジェクトの`KENALL`プロパティの値として`KENALL`コンストラクタが利用可能になります。コンストラクタに対して`new`を適用することで、`KENALL`オブジェクトを扱うことができるようになります。

```html
<script type="text/javascript">
function fill(form) {
  // APIキーはダッシュボードから取得してください
  const k = new kenall.KENALL('API_KEY_DAYO');
  const postalCode = form.elements["postalcode"].value;
  k.getAddress(postalCode).then(
    function (address) {
      const firstCandidate = address.data[0];
      form.elements["prefecture"].value = firstCandidate["prefecture"];
    }
  ).catch(function () {
    alert("API呼び出しに失敗しました");
  });
}
</script>
```

のように利用してください。

### Node.jsで使う場合

プロジェクトのディレクトリで

```
$ npm i @ken-all/kenall
```

を実行します。

```javascript
const { KENALL } = require('@ken-all/kenall');

// APIキーはダッシュボードから取得してください
const api = new KENALL('API_KEY_DAYO');

api.getAddress(postalCode).then(
  r => {
    console.log(r);
  }
).catch(
  e => {
    console.error(e);
  }
);
```

## ビルド方法

```
$ npm run build
```

を実行すると、生成されたjsファイルが`built/`配下に出力されます。

```
$ npm run bundle
```

を実行すると、ブラウザ向けバンドルファイルが`dist/`配下に出力されます。


## テスト

```
$ npm run test
```

## Examples & Demos

* [API呼び出しのサンプル (CodePen)](https://codepen.io/kenall/pen/NWbPYda)
* https://github.com/KEN-ALL/kenall-js/tree/master/examples
