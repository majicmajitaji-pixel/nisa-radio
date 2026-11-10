# 朝の米国株・NISAラジオ

ゆうべのアメリカ株と、NISAの動きを、毎朝わかりやすくお届けする番組です。

このリポジトリが、そのまま放送のページです。ビルドは要りません。`main` ブランチの中身を GitHub Pages がそのまま配信します。

聴くページ: https://majicmajitaji-pixel.github.io/nisa-radio/

スマートフォンのブラウザで開き、画面の再生ボタン（または再生バーの ▶）を一度タップすると音声が始まります。自動では再生しません。

## ファイル

```
index.html                         プレーヤー（myradio、MIT）
station.json                       局の名前、説明、ロゴ、クレジット
logo.svg                           この番組のロゴ
episodes.json                      回の一覧。先頭が最新で、トップページが再生する回
episodes/YYYY-MM-DD-ja.json        その回の台本
audio/YYYY-MM-DD-ja.mp3            その回の音声
character/                         キャスターの画像
```

パスはすべてページからの相対パスです。`https://majicmajitaji-pixel.github.io/nisa-radio/` のように、リポジトリ名の下でもそのまま動きます。先頭に `/` は付けないでください。

## 新しい回を足す

1. 直前の台本 `episodes/YYYY-MM-DD-ja.json` をコピーし、`episodes/新しい日付-ja.json` として保存する。日付は `2026-11-11` のようにハイフン区切り。
2. 中身をその日のニュースに書き換える。残す欄は次のとおり。
   - `date` … ファイル名の日付と同じ
   - `lang` … `ja`
   - `title` … その回の題
   - `opening` / `news` / `closing` … 話す文。各文は `say`（読み上げ）と `show`（画面の字幕）
   - `news[].label` … 見出し。`points` … 画面に出す要点。`lines` … その話題で話す文
   - `lines_timed` … 文ごとの `start` と `end`（秒）。字幕が音声に合う
   - `segments` … `opening` / `news` / `closing` の区切り（秒）。話題の切り替えに使う
   - `seconds` … 音声の長さ（秒）
   - `audio` … `audio/新しい日付-ja.mp3`（相対パス）
3. 読み上げた音声を `audio/新しい日付-ja.mp3` に置く。台本の `audio` と同じ名前にする。
4. `episodes.json` の**先頭**に、その回を足す。先頭の1件が、トップページで再生される最新回になる。

```json
{
  "date": "2026-11-11",
  "ja": { "title": "その回の題", "seconds": 180.0 }
}
```

5. `main` にコミットして push する。GitHub Pages が数分で同じ URL を更新する。サーバーの作業やビルドは要らない。

台本の形は、入っている `episodes/2026-11-11-ja.json` をそのまま見本にしてください。

## 毎回残すこと

締めの文に、次の免責を残してください。

> 売り買いをおすすめするものではありません。

この番組は、公開されているニュースのまとめです。売買の推奨ではありません。台本には、保有銘柄や口座、メールアドレスなど、個人の情報を書かないでください。

## 公開の設定

配信元は **`main` ブランチのルート**（`/ (root)`）です。`gh-pages` ブランチや、別のビルドは使いません。音声もこのブランチに入れます。ページを開いたブラウザが、相対パスで `audio/` の mp3 を取りにいきます。

リポジトリの Settings → Pages で、Build and deployment の Source を **Deploy from a branch**、Branch を **main**、フォルダを **/ (root)** にして保存します。反映後の URL は次です。

https://majicmajitaji-pixel.github.io/nisa-radio/

## ライセンス

- プレーヤー（`index.html`）は [myradio](https://github.com/monoradio102/myradio) をもとにしています。Copyright (c) 2026 monoradio102、MIT License。許諾文は `LICENSE` にあります。
- キャラクター画像（`character/`）は、この番組のオリジナルのAI生成キャラクターです。クレジットは `station.json` の `credits` にあり、ページの下に出ます。消さないでください。
- 局の名前とロゴ（`logo.svg`）は、この番組のものです。
- 音声は Microsoft Edge ニューラル音声（ja-JP-NanamiNeural）で作った試しの読み上げです。声の利用条件は、その音声の提供元に従ってください。
- 台本は、この番組のニュースまとめです。
