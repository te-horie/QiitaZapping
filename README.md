# QiitaZapping

## 概要

検索設定に該当する記事のザッピング(関連する記事の遷移) 支援

QiitaZapping を用いて会社の日報を読んでいる様子

<img src="./QiitaZapping.gif" width="400">

## 仕組み

- Qiita API から `検索設定` の最新記事 100 件を取得
- 現在開いている記事の前後の作成日時の記事を判定しリンク先としてアロー表示
    - 読み込み高速化のため前後記事は `prefetch` 指定

## 利用の流れ

1. ブラウザ右上の extension アイコンから検索設定を記入
1. ページ両端のアロー押下もしくはショートカットでページ遷移開始

### 1. ブラウザ右上の extension アイコンから検索設定を記入

![](./popup.png)

以下を記入。

- domain
    - `query` を適用するドメインを指定
    - `qiita.com` or `xxx.qiita.com`
- query
    - ザッピングを行う検索条件を指定
    - 例: tag:日報
    - 省略時: 最新の投稿を取得
- token
    - 発行方法: qiita のプロフィールアイコンから `設定` -> `アプリケーション` -> `個人用アクセストークン`
    - スコープ: `read_qiita` or `read_qiita_team`

最後に有効化するラジオボタンを選択して `Save` を押下。

### 2. ページ両端のアロー押下もしくはショートカットでページ遷移開始

遷移先がある場合、記事閲覧時に左端、右端にそれぞれアローが表示されます。

アロー押下もしくはショートカットから遷移が可能です。

※ ショートカットの設定

![](./shortcut.png)

- `chrome://extensions/shortcuts` にアクセス
- QiitaZapping の `go to next item`, `go to previous item` にお好みのショートカットを設定

## FAQ

### Q. アローが表示されません。

次の要因が考えられます。

- `検索設定` に誤りがある(初めてご利用の場合)。
    - ドメインは正しいですか？
    - クエリは正しいですか？
    - トークン、及びそのスコープは正しいですか？
    - ラジオボタンは正しく選択されていますか？
- 記事が古い
    - 遷移対象は `query` 指定の最新 100 件のみ対象です。
