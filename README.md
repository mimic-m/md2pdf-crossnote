# md2pdf-crossnote

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-green.svg)](https://nodejs.org/)

[crossnote](https://github.com/shd101wyy/crossnote)を使用してMarkdownファイルをPDFに変換するCLIツールです。**Markdown Preview Enhanced**と同等の高品質なレンダリング品質を提供します。

## ✨ 特徴

**crossnoteエンジンによる高品質なMarkdown→PDF変換**

- 🎯 **高品質PDF出力** - プロフェッショナルなPDF生成
- 📐 **LaTeX数式サポート** - KaTeXによる数式表現のレンダリング
- 📊 **図表・チャート** - Mermaid、PlantUMLなど多様な図表タイプに対応
- 🎨 **シンタックスハイライト** - GitHubスタイルのコードブロック装飾
- 📝 **GitHub Flavored Markdown** - テーブル、タスクリスト、拡張機能を完全サポート
- ⚡ **信頼性の高い変換** - 安定したMarkdown→PDF変換
- 🔧 **設定可能** - PDF設定（マージン、フォーマットなど）をカスタマイズ可能

## 📦 インストール

### 前提条件

- **Node.js 18+** 
- **Chrome/Chromiumブラウザ** (PDF生成用)

### 依存関係のインストール

```bash
git clone https://github.com/your-username/md2pdf-crossnote.git
cd md2pdf-crossnote
npm install
```

## 🚀 使用方法

### 基本的な使用方法

```bash
# MarkdownをPDFに変換
node bin/md2pdf examples/sample.md -o output.pdf

# カスタムPDFオプション付き
node bin/md2pdf document.md -o output.pdf --pdfOptions='{"format":"A4","margin":{"top":"25mm","right":"12mm","bottom":"25mm","left":"25mm"}}'
```

### コマンドラインオプション

```
使用方法: md2pdf <input.md> -o <output.pdf> [--pdfOptions="{...}"]

引数:
  input.md              入力Markdownファイル
  -o, --output          出力PDFファイルパス
  --pdfOptions          PDF設定オプションのJSON文字列

PDFオプション (JSON形式):
  {
    "format": "A4|Letter|Legal",
    "margin": {
      "top": "25mm",
      "right": "25mm", 
      "bottom": "25mm",
      "left": "25mm"
    }
  }
```

### 使用例

#### 基本的な変換
```bash
node bin/md2pdf README.md -o documentation.pdf
```

#### カスタムページフォーマット
```bash
node bin/md2pdf report.md -o report.pdf --pdfOptions='{"format":"A4","margin":{"top":"12mm","bottom":"12mm","left":"25mm","right":"25mm"}}'
```

#### 複数ファイルの一括変換 (bash/zsh)
```bash
for file in *.md; do
  node bin/md2pdf "$file" -o "${file%.md}.pdf"
done
```

## 📋 サポートされているMarkdown機能

**crossnoteライブラリがサポートする全機能を利用可能**

| 機能 | サポート | 備考 |
|------|----------|------|
| 見出し | ✅ | H1-H6、自動ID生成 |
| **太字**、*斜体* | ✅ | 標準強調表現 |
| `コード`ブロック | ✅ | シンタックスハイライト |
| テーブル | ✅ | GitHubスタイルテーブル |
| リンク | ✅ | 自動リンク・参照リンク |
| 画像 | ✅ | ローカル・リモート画像 |
| リスト | ✅ | 番号付き・番号なし・タスクリスト |
| 引用 | ✅ | ネストした引用 |
| 数式 | ✅ | `$$` LaTeX式をKaTeXでレンダリング |
| 図表 | ✅ | Mermaid、PlantUMLなど |
| HTML | ✅ | 埋め込みHTML要素 |

## 🔧 開発

### プロジェクト構造

```
md2pdf-crossnote/
├── bin/
│   └── md2pdf              # メインCLIスクリプト
├── examples/               # サンプルファイル
│   └── sample.md          # 機能テスト用サンプル
├── dist/                   # ビルド済み実行可能ファイル
├── package.json           # 依存関係とスクリプト
└── README.md              # このファイル
```

### 実行可能ファイルのビルド

```bash
# Windows実行可能ファイルをビルド
npm run build:win

# Linux実行可能ファイルをビルド
npm run build:linux
```

**注意**: crossnoteの依存関係にはネイティブモジュールが含まれるため、実行可能ファイルのビルドは複雑です。Node.jsスクリプトでの実行を推奨します。

### テスト

```bash
# サンプルファイルでテスト
node bin/md2pdf examples/sample.md -o test-output.pdf

# カスタムオプションでテスト
node bin/md2pdf examples/sample.md -o custom.pdf --pdfOptions='{"format":"A4","margin":"12mm"}'
```

## ⚙️ 設定

### PDFオプション

すべてのPDFオプションは`--pdfOptions`パラメータにJSONとして渡します：

```json
{
  "format": "A4",
  "landscape": false,
  "margin": {
    "top": "25mm",
    "right": "25mm",
    "bottom": "25mm", 
    "left": "25mm"
  },
  "printBackground": true,
  "preferCSSPageSize": false
}
```

### 環境変数

- `PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=1` - ChromiumのダウンロードをスキップしてシステムのChromeを使用
- `CHROME_BIN` - Chrome/Chromium実行可能ファイルのパス（PATHにない場合）

## 🐛 トラブルシューティング

### よくある問題

**"Chrome/Chromiumが見つかりません"**
```bash
# Chrome/Chromiumをインストール
# Ubuntu/Debian
sudo apt-get install chromium-browser

# macOS  
brew install --cask google-chrome

# Windows - https://www.google.com/chrome/ からダウンロード
```

**"ブラウザの起動に失敗しました"**
```bash
# Chromeのパスを明示的に設定
export CHROME_BIN="/usr/bin/google-chrome"
node bin/md2pdf sample.md -o output.pdf
```

**"数式が正しくレンダリングされない"**
- LaTeX式が`$$`または`$`で囲まれていることを確認
- 使用している数学記法がKaTeXでサポートされているか確認

**"PDF変換に失敗する"**
- crossnoteとPuppeteerの設定を確認してください
- Chrome/Chromiumが正しくインストールされているか確認してください

### デバッグモード

デバッグ出力付きで実行：
```bash
DEBUG=crossnote* node bin/md2pdf examples/sample.md -o output.pdf
```

## 🤝 貢献

コントリビューションを歓迎します！プルリクエストをお気軽にお送りください。

### 開発環境のセットアップ

1. リポジトリをフォーク
2. フォークをクローン: `git clone https://github.com/mimic-m/md2pdf-crossnote.git`
3. 依存関係をインストール: `npm install`
4. 変更を加える
5. テスト: `node bin/md2pdf examples/sample.md -o test.pdf`
6. プルリクエストを提出

### 問題の報告

以下の情報を含めてください：
- オペレーティングシステムとバージョン
- Node.jsバージョン
- Chrome/Chromiumバージョン
- 問題を再現するサンプルMarkdownファイル
- 完全なエラーメッセージとスタックトレース

## 📄 ライセンス

このプロジェクトはMITライセンスの下でライセンスされています - 詳細は[LICENSE](LICENSE)ファイルをご覧ください。

## 🙏 謝辞

- [crossnote](https://github.com/shd101wyy/crossnote) - これを可能にした強力なMarkdownエンジン
- [Markdown Preview Enhanced](https://shd101wyy.github.io/markdown-preview-enhanced/) - 高品質Markdownレンダリングのインスピレーション

## 🔗 関連プロジェクト

- [Markdown Preview Enhanced](https://github.com/shd101wyy/markdown-preview-enhanced) - VSCode/Atom拡張機能
- [crossnote](https://github.com/shd101wyy/crossnote) - コアライブラリ

---

⭐ このプロジェクトがお役に立ちましたら、スターをお願いします！
