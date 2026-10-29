# Demography Working Group ウェブサイト

公開URL：<https://dwg-utokyo.github.io/>

[Quarto](https://quarto.org/) で作成し、GitHub Pages で公開する DWG のウェブサイトです。

## ファイル構成

```
_quarto.yml            サイト全体の設定（タイトル・メニュー・テーマ）
styles.scss            デザイン（色・フォント）
index.qmd              トップページ（今後のセミナー・お知らせ・主な活動）
about.qmd              研究会について（目的・活動内容・運営体制・沿革）
projects.qmd           研究プロジェクト（準備中。追加方法はファイル内のコメント参照）
join.qmd               参加について（参加対象・加入の流れ・問い合わせ）
en.qmd                 英語ページ（概要・運営メンバー・参加方法。about.qmd / join.qmd を変えたら合わせて更新）
_upcoming.qmd          今後のセミナー予定（トップページと年度ページに差し込まれる）
seminars/
  fy2025.qmd           2025年度の活動記録（2025年4月〜2026年3月）
  fy2026.qmd           2026年度の活動記録（2026年4月〜2027年3月）
images/                画像置き場（サイトで使うのは logo.png・logo-mark.png・favicon.png）
dwg-website.Rproj      RStudio のプロジェクトファイル
.github/workflows/     GitHub Pages への自動デプロイ設定
```

## ローカルでの確認

1. Quarto をインストール：<https://quarto.org/docs/get-started/>
2. このフォルダで次を実行すると、ブラウザでプレビューが開きます（終了は Control + C）。

   ```sh
   quarto preview
   ```

RStudio を使う場合は `dwg-website.Rproj` を開き、Build タブの「Render Website」でサイト全体を作成できます。

## 今後の予定の更新

予定は `_upcoming.qmd` の1か所に書きます（トップページと年度ページの両方に表示されます）。

- 3か月ごとの日程調整後：予定を新しいものに書き換え、期間と更新日も直す（書き方はファイル冒頭のコメント参照）
- 開催が終わったら：その回のブロックを削除し、次の「セミナー記録の追加」を行う
- 会場は掲載しない

## セミナー記録の追加

1. その年度のページ（例：`seminars/fy2026.qmd`）を開く
2. 「これまでの記録」の冒頭のコメントにある形式で、**最新回を一番上に**書き足す
3. 必要に応じてトップページの「お知らせ」を更新する

### 新しい年度になったら

1. 前年度のファイルをコピーして `seminars/fy2027.qmd` のように名前を変え、タイトル・期間を書き換えて中身を空にする
2. `_quarto.yml` の「活動記録」メニューに新しい年度を一番上に追加する
3. トップページ（`index.qmd`）と `join.qmd` の活動記録へのリンクを新年度に変える
4. 「今後の予定」欄（`{{< include ../_upcoming.qmd >}}` の部分）を新年度のページに移す

## GitHub Pages での公開（初回のみ）

1. 自動デプロイ設定を所定の場所へ移動する（`_setup/publish.yml` → `.github/workflows/publish.yml`）

   ```sh
   mkdir -p .github/workflows
   mv _setup/publish.yml .github/workflows/publish.yml
   rmdir _setup
   ```

2. GitHub の Organization（dwg-utokyo）に `dwg-utokyo.github.io` という名前の公開リポジトリを作成する（README などは追加しない）
3. リポジトリの **Settings → Pages → Build and deployment → Source** を **GitHub Actions** に設定
4. このフォルダの中身を `main` ブランチに push

   ```sh
   git init -b main
   git add .
   git commit -m "Initial site"
   git remote add origin https://github.com/dwg-utokyo/dwg-utokyo.github.io.git
   git push -u origin main
   ```

以後は `main` に push するたびに自動でサイトが更新されます（Actions タブで進捗を確認できます）。

## 注意

GitHub Pages のサイトは誰でも閲覧できます。メーリングリスト・Slack の招待リンクは掲載しないでください。報告資料（スライド等）は公開しない方針です。
