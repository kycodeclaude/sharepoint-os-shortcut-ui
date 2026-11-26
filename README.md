# SharePoint OS - ショートカット管理UI

SharePoint を、デスクトップ風の画面（左：ショートカット、右：今のフォルダ）で使うための Tampermonkey 用ユーザースクリプトです。

> ⚠️ 非公式ツールです。Microsoft とは関係ありません。SharePoint 側の画面や内部 API が変わると、動かなくなることがあります。

## 主な機能（初期設定＝ライトモードで使えるもの）

- ショートカット管理（カテゴリ分け・色分け・並べ替え・お気に入り・最近開いたもの）
- サイト全体検索、ファイルのプレビュー窓
- ごみ箱・操作ログ（取り消し）・容量の確認（版の調査を含む）
- ショートカットの健全性チェック（リンク切れ・権限なし・重複）
- 設定の全バックアップ／復元
- タッチモード（スマホ・タブレット向け）、長押し＝右クリック

## ライトモード（v1.1.0〜の初期設定）

ふだん使わない機能は、**初めはオフ**です。🎨「テーマ」窓の「🧩 機能の切替」でオンにできます。

| 項目 | 初期設定 | 内容 |
|---|---|---|
| ⚡ 動く演出 | オフ | 動く背景・起動演出・クリック演出・警告演出・ティッカー |
| 🔷 3Dビュー | オフ | 左上「ショートカット管理エリア」の文字クリックで開く。切替後は再読み込みが必要 |
| 🎨 すべてのテーマ | オフ | オフのあいだは、標準・定番配色・大人向け・工場向けだけを一覧に表示 |

※ 1.0.0 から更新した場合、動く演出と3Dビューは自動でオフになります。使いたいときは上の切替でオンにしてください。

## 言語（日本語／English）v1.2.0〜

- 初回はブラウザの言語で決まります（日本語以外は English）
- 切り替えは、🎨「テーマ」窓の「🧩 機能の切替」にある「🌐 言語 / Language」から。ページの再読み込みで反映されます
- 翻訳されるのは主要な画面の文言です。奥のダイアログなど、一部は日本語のまま残ります

## 「最新の日付シートを確認」の対象 v1.2.0〜

- 初期設定では、すべての xlsx/xlsm が対象です
- 名前に特定の語を含むブックだけに絞る場合は、🎨「テーマ」窓の「🧩 機能の切替」にある「対象キーワード」に語を入れてください（大文字小文字は区別しません）

## インストール

1. ブラウザに [Tampermonkey](https://www.tampermonkey.net/) を入れます。
2. **[インストールはこちら](https://raw.githubusercontent.com/kycodeclaude/sharepoint-os-shortcut-ui/main/SharePoint_OS_ShortcutUI_public.user.js)** を開くと、Tampermonkey のインストール画面が出ます。そのまま「インストール」を押してください。
3. `https://〇〇.sharepoint.com/` を開きます。

更新は、Tampermonkey が GitHub の最新版を自動で確認して届けます（v1.2.2〜）。

> [Greasy Fork](https://greasyfork.org/ja/scripts/607402-sharepoint-os-%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88%E7%AE%A1%E7%90%86ui) にも掲載しています（データファイルを分離した v1.3.0 以降）。

## このスクリプトが行うこと（通信・権限・保存）

### 通信先
- いま開いている SharePoint（`〇〇.sharepoint.com`）の REST API（`/_api/...`）
- 同じテナントの個人 OneDrive（`〇〇-my.sharepoint.com`）。ページからの通信は CORS で拒否されるため、この間だけ `GM_xmlhttpRequest` で通信します
- **外部のサーバーへ、データを送信することはありません。**
- Outlook・Teams・Microsoft 365 は、スタートメニューの「リンク集」としてURLを持っているだけです（クリックしたときに開きます）

### Tampermonkey の権限
- `GM_xmlhttpRequest`：上記の、SharePoint ⇄ 個人 OneDrive の通信のみ
- `unsafeWindow`：ページ側の `_spPageContextInfo`（サイトURL・ユーザー情報）を読むため
- `@connect sharepoint.com`
- ページ側の `fetch` を書き換えてはいません。スクリプト内だけで、上記の通信を振り分ける `fetch` を使っています

### 保存するデータ（ブラウザ内のみ）
- `localStorage`：キーは `osDesktop…`・`osx_…`・`osGlass3d…`・`osOpen…`・`osOffice…` で始まります（ショートカット・カテゴリ・テーマ・お気に入り・操作ログ・ごみ箱の控え など）
- `IndexedDB`：`sharepoint-os-cache`（サムネイルのキャッシュ）
- 「全設定バックアップ」で、設定をファイルに出力・復元できます

### 診断
- F12 のコンソールで `localStorage.setItem('osxDebug_v1','1')` を実行して再読み込みすると、デバッグ用のログが出ます（止めるときは `removeItem`）

## 既知の制限
- SharePoint の DOM・内部 API の仕様変更に弱いです
- 1ファイルが大きいため（約3.4万行）、起動時の読み込みに時間がかかる環境があります

## ライセンス
MIT（`@license` に記載。変更する場合は、スクリプト先頭と、この欄を合わせて直してください）

## 不具合・要望
GitHub Issues へお願いします（URLはスクリプト先頭の `@supportURL`）。報告には、次の情報があると助かります。
- ブラウザと Tampermonkey のバージョン、スクリプトのバージョン（スタートメニューの更新履歴で確認）
- 開いていた画面（SharePoint／個人 OneDrive）と、操作の手順
- F12 コンソールのエラー表示（`osxDebug_v1` をオンにした状態だと詳しく出ます）

## 更新方針
- 個人で開発・保守しています。SharePoint 側の変更による不具合は、確認でき次第、修正します（対応の時期は約束できません）
- 寄付やスターをいただけると、バージョンアップの励みになります

## 応援・寄付
個人で開発・保守しています。役に立ったら、コーヒー1杯分の応援をいただけると励みになります。もちろん無理のない範囲で大丈夫です。
☕ Ko-fi: https://ko-fi.com/kycodeclaude

## Support
Developed and maintained by one person in my spare time. If it helps your work, a small tip would be much appreciated — only if you feel like it.
☕ Ko-fi: https://ko-fi.com/kycodeclaude
