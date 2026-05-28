# D-SMART デザインシステム

D-SMART 業務システム（2000年代 ASP/JSP）のASIS画面を再現するためのCSSテンプレートとHTMLスニペット集。

---

## 設計思想

**Web 1.0 業務系 / Windows XP Classic 風**

- HTMLテーブルレイアウトによる画面構成
- Windows 98/XP Classic テーマに準拠したUI部品
- フォント: MS Pゴシック 系 / 12px ベース
- 全パーツで同一グレー `#C8C8C8` を使用し、ボーダーのみで区画を表現

---

## ファイル構成

```
_dsmart-design-system/
├── dsmart-base.css          # 全共通スタイル（必ずリンクする）
├── components/
│   ├── sidebar.html         # サイドバー HTMLスニペット
│   └── screen-header.html   # 画面ヘッダーバー HTMLスニペット（プレースホルダー付き）
└── README.md                # 本ファイル
```

---

## カラーパレット

| 用途 | カラーコード | 使用箇所 |
|------|-------------|---------|
| グレー背景 | `#C8C8C8` | ボタン / thead / .lbl / .sub-title-row / .submit-bar |
| ボーダー標準 | `#808080` | テーブル枠 / .sep / .screen-header |
| ボーダー薄 | `#999999` | input / textarea / select の外枠 |
| 入力背景 | `#FFFFFF` | td デフォルト / input / textarea / select テキスト部 |
| 画面ヘッダー | `#003399` | .screen-header 背景 |
| 必須マーク | `#CC0000` | .req（※マーク） |
| テキストリンク | `#0000CC` | .btn-link |
| ユーザーバー | `#6699CC` | .sidebar-username |

---

## UIパーツ一覧

### レイアウト

| クラス | 説明 |
|--------|------|
| `.layout` | flex コンテナ（サイドバー + メイン） |
| `.main` | メインコンテンツ領域 |
| `.content-wrap` | フォームコンテンツの幅制御（820px） |
| `.form-box` | フォーム外枠（ボーダーなし・白背景） |

### サイドバー

| クラス | 説明 |
|--------|------|
| `.sidebar` | サイドバー全体（幅190px） |
| `.sidebar-logo` | ロゴエリア |
| `.logo-text` / `.logo-d` | DSMARTロゴテキスト（D=青 / SMART=赤） |
| `.sidebar-username` | ログインユーザー名（青帯） |
| `.sidebar-buttons` | TOP/HELP/MY PORTAL/終了 ボタングリッド |
| `.sidebar-btn` | サイドバーナビボタン |
| `.sidebar-dept` | 部署名（ピンク帯） |
| `.sidebar-date` | 日付（青帯） |
| `.sidebar-menu-close` | メニューを閉じるリンク |
| `.sidebar-links` | メニューリンクスクロールエリア |
| `.sidebar-links a.indent` | 階層インデントリンク |

### 画面ヘッダーバー

| クラス | 説明 |
|--------|------|
| `.screen-header` | 青い画面ヘッダーバー全体 |
| `.section-mark` | § マーク（黄色） |
| `.screen-id` | 画面ID表示（右寄せ薄色） |

### フォーム入力要素

| セレクタ | 説明 |
|----------|------|
| `input[type="text"]` / `input[type="number"]` | テキスト入力（inset shadow で凹み枠） |
| `textarea` | テキストエリア（同上 / セル内フル幅は `border:none` で上書き） |
| `select` | ドロップダウン（SVGで Windows XP 風 ▼ ボタンを再現） |
| `input[type="checkbox"]` | チェックボックス（左上濃/右下淡ボーダーで凹み枠） |

### ボタン

| クラス | 説明 |
|--------|------|
| `.btn` | 標準ボタン（3Dベベル / 押下でボーダー反転） |
| `.btn-cal` | カレンダー選択ボタン「...」（小型） |
| `.btn-link` | テキストリンク風ボタン |

### テーブル & 区画

| クラス / セレクタ | 説明 |
|------------------|------|
| `table.form-table` | フォームテーブル共通（border-collapse） |
| `table.form-table th` | ヘッダーセル（グレー背景） |
| `table.form-table td` | データセル（白背景） |
| `.lbl` | ラベルセル（グレー背景・td に付与） |
| `.sub-title-row` | セクション区切りタイトル行（div に付与） |
| `.sep` | 水平区切り線（hr に付与） |
| `.req` | 必須マーク ※（赤） |

### ユーティリティ

| クラス | 説明 |
|--------|------|
| `.note-red` | 赤い注記テキスト（11px） |
| `.note-black` | 黒い注記テキスト（11px） |
| `.submit-bar` | 画面下部 登録ボタンバー（グレー帯） |

---

## 新しいASIS画面の作り方

### 1. HTMLのひな型をコピーする

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>{{画面名}} - ASIS</title>
<link rel="stylesheet" href="../_dsmart-design-system/dsmart-base.css">
</head>
<body>
<div class="layout">

  <!-- サイドバー（components/sidebar.html からコピー） -->
  <div class="sidebar">
    ...
  </div>

  <!-- メインコンテンツ -->
  <div class="main">

    <!-- 画面ヘッダー（components/screen-header.html からコピーして置換） -->
    <div class="screen-header">
      <span class="section-mark">§</span>{{画面名}}
      <span class="screen-id">[ {{画面ID}} ]</span>
    </div>

    <div class="content-wrap">
    <div class="form-box">

      <!-- ① セクション見出し -->
      <div class="sub-title-row">セクション名</div>

      <!-- ② フォームテーブル -->
      <table class="form-table">
        <tr>
          <td class="lbl" style="width:80px;">ラベル<span class="req">※</span></td>
          <td><input type="text" style="width:200px;"></td>
        </tr>
      </table>

      <hr class="sep">

      <!-- ③ 登録ボタンバー -->
      <div class="submit-bar">
        <span>合計&nbsp;<strong>0</strong></span>
        <button class="btn">登録</button>
      </div>

    </div><!-- /form-box -->
    </div><!-- /content-wrap -->

  </div><!-- /main -->
</div><!-- /layout -->
</body>
</html>
```

### 2. よく使うパターン

**ラベル + 入力行**
```html
<table class="form-table">
  <tr>
    <td class="lbl" style="width:80px;">項目名<span class="req">※</span></td>
    <td><input type="text" style="width:300px;"></td>
  </tr>
</table>
```

**セクションヘッダー付きテーブル**
```html
<div class="sub-title-row">セクション名</div>
<table class="form-table">
  <thead>
    <tr>
      <th style="width:40px;">No</th>
      <th>項目A</th>
      <th>項目B</th>
      <th style="width:80px;"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center; background:#C8C8C8;">1</td>
      <td><input type="text" style="width:98%;"></td>
      <td><select style="width:100px;"><option>選択肢</option></select></td>
      <td style="background:#C8C8C8; text-align:right;">
        <button class="btn">更新</button>
        <button class="btn">削除</button>
      </td>
    </tr>
  </tbody>
</table>
<div style="padding:3px 5px;">
  <button class="btn">行追加</button>
</div>
```

**日付入力セル（カレンダーボタン付き）**
```html
<td>
  <input type="text" style="width:82px;" value="2011/06/28">
  <button class="btn-cal">...</button>
</td>
```

**セル内フル幅テキストエリア（枠なし）**
```html
<td style="padding:1px;">
  <textarea style="width:100%; height:60px; border:none; box-shadow:none; background:#fff;">テキスト内容</textarea>
</td>
```

**注記テキスト**
```html
<span class="note-red">※必須項目です。</span>
<span class="note-black">参考情報テキスト</span>
```

---

## 実装済み画面

| ファイル | 画面名 | 画面ID |
|----------|--------|--------|
| [出張精算情報を登録する/asis_chossei_input.html](../出張精算情報を登録する/asis_chossei_input.html) | 出張精算入力 | GPOR21009 |

---

## 注意事項

- `dsmart-base.css` へのパスは各HTMLから相対パスで指定する
- インライン `style=""` は幅指定など画面固有の微調整にのみ使用する
- `background:#C8C8C8` をインラインで使うのは非入力セル（No列・ボタン列）のみ
- セル内フル幅テキストエリアは `border:none; box-shadow:none` を上書きして使う
