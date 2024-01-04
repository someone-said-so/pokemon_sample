# このリポジトリについて

このリポジトリはAndroidでのテストコードとJetpack Composeを学習するためのリポジトリです。  

# アプリの機能

- ホームタブで[PokeAPI](https://pokeapi.co/)のポケモンをリスト表示する
- ポケモンは無限スクロールで追加読み込みを行う
- 3匹までのポケモンをモンスターボールに捕獲しておき、ボールタブで詳細を確認できる
- 設定タブで利用規約を確認できる
- アプリインストール直後の起動でランダムなUUIDを生成してUIDとして永続化し、Firebase Analylytics（以下、FA）のセグメントに設定
- 捕獲/解放を行った時にFAのイベントを送信

# 設計について

このリポジトリではテストを容易にするために以下の対応を行っている。

- hiltによるDIコンテナで依存関係逆転を行い、テストの際はインターフェースに注入するものを差し替え（オーバーライド）する
- MockitoでFAのように外部へのインターフェース定義されていないサードパーティーライブラリでもテストできるようにする
- UUIDや日付などの外部環境依存するものはファクトリーをインターフェース定義し、テストの際にオーバーライドできるようにする
- 非同期についてはJetpack Composeとユニットテストの実装で相性の良いCoroutineで実装する

| 機能 | ライブラリ |
| --- | --- |
| HTTPクライアント | OkHttp |
| ローカルDB | Room |
| JSONコーダー | kotlinx-serialization |
| アプリ計測 | FA |