# GitHub Pagesで公開する手順

対象リポジトリは [qua2000/smartphone-starry-sky](https://github.com/qua2000/smartphone-starry-sky) です。このリポジトリは**公開（Public）**で、トップ階層に `index.html` があるため、GitHub Pagesでそのまま公開できます。現在はまだGitHub Pagesの公開設定が作成されていない状態です。

公開が完了すると、PC・スマホ共通で次のURLから開けるようになります。

> **公開予定URL:** `https://qua2000.github.io/smartphone-starry-sky/`

## まず知っておくこと

GitHub Pagesは、リポジトリ内のHTML、CSS、JavaScriptをWebサイトとして公開する機能です。今回のようにビルド作業が不要な単純なHTMLページは、`main` ブランチの一番上の階層（`/(root)`）を公開元に選ぶ方法が最も分かりやすく、GitHubもその方法を案内しています。[1]

| 今回の設定項目 | 選ぶ内容 | 理由 |
|---|---|---|
| 公開元（Source） | `Deploy from a branch` | HTMLをそのまま公開するため |
| ブランチ（Branch） | `main` | 現在のアプリのファイルが保存されているため |
| フォルダー（Folder） | `/(root)` | `index.html` がリポジトリの一番上にあるため |

## 公開の操作手順

PCのブラウザでGitHubへサインインし、次のリンクを開いてください。

> [スマホ星空リポジトリを開く](https://github.com/qua2000/smartphone-starry-sky)

開いたら、以下の順番で操作します。

| 手順 | 画面で行うこと | 選ぶ内容・確認すること |
|---|---|---|
| 1 | リポジトリ上部の **Settings** をクリックする | 見つからない場合は、上部の `…`（More）メニューを開く |
| 2 | 左側のメニューを下へ見て **Pages** をクリックする | `Code, planning, and automation` の中にあります |
| 3 | `Build and deployment` の `Source` をクリックする | **Deploy from a branch** を選ぶ |
| 4 | `Branch` の最初の選択欄をクリックする | **main** を選ぶ |
| 5 | 右側のフォルダー選択欄をクリックする | **/(root)** を選ぶ |
| 6 | **Save** をクリックする | この時点で公開処理が始まります |

操作が成功すると、同じPages画面に「Your site is live at …」のような表示、または `Visit site` ボタンが現れます。そのリンクをクリックしてサイトを開ければ公開成功です。

## 公開後の確認方法

初回公開では反映に数分かかることがあります。GitHubの案内では、反映に最大10分ほどかかる場合があります。[2] `Visit site` がまだ出ない場合は、すぐに設定をやり直さず、数分待ってからPages画面を再読み込みしてください。

公開後は、PCでもスマホでも次のURLを開きます。

```text
https://qua2000.github.io/smartphone-starry-sky/
```

| 端末 | 確認すること | 補足 |
|---|---|---|
| PC | ページの見た目、各ボタン、現在時刻が表示されるか | PCにカメラがあれば、ブラウザの許可後にカメラ映像も確認できます |
| Androidスマホ | カメラ、位置情報、端末の向き、月の予測位置、Moon表示 | これまでの実機確認と同じ順番で使えます |
| iPhone | カメラと位置情報、向きの許可画面 | 端末の向きはSafariの設定・許可により挙動がAndroidと異なる場合があります |

カメラと位置情報を使うWeb機能には、利用者の許可と安全な接続（HTTPS）が必要です。GitHub Pagesの標準URLはHTTPSのため、このアプリに適した公開方法です。[3] [4]

## 更新したときの流れ

今後、GitHubへ変更を保存して `main` ブランチへ反映すると、GitHub Pagesも自動で新しい内容を公開します。公開設定を一度行えば、毎回Pagesの設定画面を開く必要はありません。[1]

| したいこと | 基本の流れ |
|---|---|
| コードを変更する | ファイルを編集する |
| 変更をGitHubへ保存する | `git add` → `git commit` → `git push` を行う、またはGitHub画面で編集して `Commit changes` を押す |
| 公開ページへ反映する | 数分待ち、公開URLを再読み込みする |

## うまくいかないとき

| 状況 | まず試すこと |
|---|---|
| `Settings` が見当たらない | 上部の `…` メニューを開き、Settingsを探す。リポジトリの管理権限がない場合は設定できません |
| `Pages` が見当たらない | Settings左側のメニューを下へスクロールし、`Code, planning, and automation` を探す |
| `Visit site` が出ない | `main` と `/(root)` が選ばれているか確認し、数分待ってから再読み込みする |
| 公開URLが404になる | URL末尾の `/` を含めて開き、Pages設定と公開処理の完了を確認する |
| スマホでカメラが動かない | URLが `https://` で始まることを確認し、Chromeのカメラ許可を確認する |
| 位置情報が出ない | Chromeの位置情報許可と、スマホ本体の位置情報設定を確認する |

## 公開前の注意

GitHub Pagesで公開したページはインターネット上で誰でも閲覧できます。リポジトリが非公開の場合でも、GitHub Pagesの公開ページ自体は公開される場合があるため、住所、APIキー、パスワード、個人写真、位置情報の記録などはファイルに保存・掲載しないでください。[1]

現在のアプリは、位置情報を月の位置の計算に使いますが、サーバーへ保存・送信する処理は含んでいません。なお、GitHub Pagesの訪問時には、セキュリティ目的でGitHubが訪問者のIPアドレスを記録します。[5]

## 参考資料

[1]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site "GitHub Docs: Configuring a publishing source for your GitHub Pages site"
[2]: https://docs.github.com/pages/quickstart "GitHub Docs: Quickstart for GitHub Pages"
[3]: https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia "MDN Web Docs: MediaDevices.getUserMedia()"
[4]: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API "MDN Web Docs: Geolocation API"
[5]: https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages "GitHub Docs: What is GitHub Pages?"
