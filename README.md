# README

Zendesk の記事に textlint を適用するためのリポジトリです。

## 必要な環境

- Git
- Node.js LTS 版

## 手順

### 初回のみ

リポジトリをクローンします。

```shell
git clone https://github.com/cybozudevnet/devnet-sample-textlint.git
```

### 記事に textlint を適用する

1. Zendesk の記事の編集画面で、[**</>**]をクリックします

1. 表示される HTML をクリップボードにコピーします

1. `content/article.html`の内容を、クリップボードの内容で差し替えます

1. クローンしたリポジトリのディレクトリーで、次のコマンドを実行します。

    ```shell
    npm install
    ```

1. 次のコマンドで、textlint を実行します。

    ```shell
    npm run lint
    ```

1. textlint の実行結果に応じて、対応します

    **textlint のチェック項目に違反する表現がない場合**  
    次のように、指摘された箇所が出力されない場合には、対応の必要はありません。

    ```shell
    npm run lint

    > devnet-sample-textlint@0.0.1 lint
    > textlint content/article.html
    ```

    **textlint のチェック項目に違反する表現がある場合**  
    実行結果に、「✖ n problem」のように指摘数が表示されます。  
    指摘された箇所を修正してください。  
    修正方法の詳細は、[textlint で指摘された箇所の対応方法](#fix) を参照してください。

    ```shell
    npm run lint

    > devnet-sample-textlint@0.0.1 lint
    > textlint content/article.html

    /Users/foo/devnet-sample-textlint/content/article.html
      3:6  ✓ error  ご紹介します => 紹介します
    過剰な敬語です  prh
      4:41  error    一文に二回以上利用されている助詞 "が" がみつかりました。  no-doubled-joshi

    ✖ 2 problem (2 error, 0 warnings)
    ✓ 1 fixable problem.
    ```

## textlint で指摘された箇所の対応方法 {#fix}

指摘の内容によって、対応方法が異なります。

- [自動で修正できる場合](#fix-auto)  
  指摘された箇所に「✓」が表示される場合には、自動で修正できます
- [手動で修正する場合](#fix-manually)

### 自動で修正できる場合 {#fix-auto}

次のように、「✓」がついている指摘箇所は、fix コマンドで修正できます。

```shell
/Users/foo/devnet-sample-textlint/content/article.html
  3:6  ✓ error  ご紹介します => 紹介します
過剰な敬語です  prh
```

1. 次のコマンドを実行します

    ```shell
    npm run fix
    ```

    指摘された箇所が、自動で修正されます。  

    ```shell
    npm run fix

    > devnet-sample-textlint@0.0.1 lint
    > textlint content/article.html
      3:3  ✔   ご紹介します => 紹介します
    過剰な敬語です  prh

    ✔ Fixed 1 problem
    ```

1. 次のコマンドを実行して、チェック項目に違反する表現がなくなるまで、自動または手動の修正作業を繰り返します

    ```shell
    npm run lint
    ```

### 手動で修正する場合 {#fix-manually}

次のように、「✓」がついてない指摘箇所は、指摘の内容を確認して、手動で修正します。

```shell
/Users/foo/devnet-sample-textlint/content/article.html
  4:41  error  一文に二回以上利用されている助詞 "が" がみつかりました。  no-doubled-joshi
```

上記の例の場合は、4 行目の文で、2 回以上「が」が出現していることを指摘されています。  
表現を見直して、指摘されないように修正します。

修正したら、次のコマンドを実行します。  
チェック項目に違反する表現がなくなるまで、自動または手動の修正作業を繰り返します。、チェック項目に違反する表現が残っていないことを確認します。

    ```shell
    npm run lint
    ```
