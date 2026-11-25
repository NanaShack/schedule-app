# スケジュール帳

月の予定（日記・出来事まとめつき）、時間割（予定・実績・比較）、家事とToDo、睡眠の記録をまとめて管理するウェブアプリです。
Googleアカウントでログインすると、PCとスマホで同じデータが見られます。

## ファイル

| ファイル | 内容 |
|---|---|
| `index.html` | アプリ本体 |
| `firebase-config.js` | Firebase の接続設定（下の手順で値を入れる） |
| `firestore.rules` | データベースのルール（本人だけが読み書きできる） |
| `manifest.webmanifest`, `sw.js`, `icons/` | ホーム画面に追加するための設定とアイコン |
| `vendor/htm-preact.js` | 画面を作るためのライブラリ（htm 3.1.1 + Preact） |
| `okikae/` | 置き換えごはん帳（三食・間食・体重の記録）。`https://nanashack.github.io/schedule-app/okikae/` で開く |

## Firebase の準備（初回だけ）

1. https://console.firebase.google.com を開き、Googleアカウントでログインして「プロジェクトを作成」
   - 名前は `schedule-app` など。Google アナリティクスはオフで構いません。
2. **ウェブアプリを登録**：プロジェクトのトップで `</>`（ウェブ）を押し、名前を入れて登録
   - 表示される `firebaseConfig` の値を `firebase-config.js` に入れます。
3. **ログインを有効にする**：左メニュー「構築」→「Authentication」→「始める」→「Google」を有効にして保存
4. **ログインを許可するドメインを追加**：Authentication の「設定」→「承認済みドメイン」に `nanashack.github.io` を追加
5. **データベースを作る**：「構築」→「Firestore Database」→「データベースを作成」
   - 場所は `asia-northeast1（東京）` がおすすめ。「本番環境モード」で作成します。
6. **ルールを設定**：Firestore の「ルール」タブに `firestore.rules` の内容を貼り付けて「公開」

`firebase-config.js` の値はブラウザに公開される前提の接続用の値で、秘密の鍵ではありません。
データを守るのは手順6のルールです。

## GitHub Pages で公開する

1. リポジトリの「Settings」→「Pages」
2. 「Build and deployment」の Source を「Deploy from a branch」、Branch を `main` / `/(root)` にして「Save」
3. 数分後に `https://nanashack.github.io/schedule-app/` で開けます

## スマホのホーム画面に追加する

- iPhone（Safari）：共有ボタン →「ホーム画面に追加」
- Android（Chrome）：メニュー →「ホーム画面に追加」または「アプリをインストール」

## claude.ai 版からデータを移す

1. claude.ai 版の「設定」→「データを書き出す」でファイルを保存
2. このアプリにログインして「設定」→「データを読み込む」でそのファイルを選ぶ

## 置き換えごはん帳（okikae/）

夕飯の置き換えダイエット用に、三食・間食・体重を記録するアプリです。
スケジュール帳と同じ Firebase プロジェクトとGoogleアカウントを使い、データは `users/<自分のID>/okikae` に保存されます。
今の `firestore.rules`（本人だけが `users/<自分のID>/` の下を読み書きできる）のままで使えるので、Firebase 側の追加設定はいりません。
ホーム画面には `https://nanashack.github.io/schedule-app/okikae/` を開いてから追加します。
