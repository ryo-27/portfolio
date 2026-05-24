# ryo-27 Portfolio

エンジニア、社会福祉、ビジネス、研究の4つの領域を横断した活動を可視化するポートフォリオサイト。

## 特徴

- **領域横断的な展示**: 4つの活動領域（エンジニア、社会福祉、ビジネス、研究）をカオスマップで可視化
- **プロジェクトベースの情報管理**: JSON形式でプロジェクト情報を一元管理
- **柔軟な画像配置**: セクション単位で画像とテキストを自由にレイアウト
- **レスポンシブデザイン**: モバイル・タブレット・デスクトップに完全対応
- **シングルファイル構成**: HTMLファイルとJSONだけで動作

## 技術スタック

- **Frontend**: Vanilla JavaScript (CDN Tailwind CSS)
- **Styling**: Tailwind CSS v3 + Custom CSS
- **Icons**: Devicon v2.15.1
- **Fonts**: Google Fonts (Inter + Noto Sans JP)
- **Data Management**: JSON format
- **Visualization**: Canvas-based Venn diagram for chaos map
- **Deployment**: Static site (Netlify, Vercel, GitHub Pages対応)

## ディレクトリ構造

```
portfolio/
├── sample.html                          # メインのポートフォリオサイト
├── public/
│   └── projects/
│       ├── projects.json               # プロジェクト詳細情報（統括管理）
│       ├── p1/
│       │   ├── main.jpg
│       │   ├── dashboard.jpg
│       │   └── system-overview.jpg
│       ├── p2/
│       │   └── collaboration.jpg
│       ├── p6/
│       │   └── llm-system.jpg
│       ├── p15/
│       │   └── visualization.jpg
│       └── ...（その他プロジェクト）
└── README.md                            # このファイル
```

## クイックスタート

### 環境構築

1. リポジトリをクローン
```bash
git clone https://github.com/ryo-27/portfolio.git
cd portfolio
```

2. ローカルサーバーで起動
```bash
# Python 3の場合
python -m http.server 8000

# Node.jsの場合
npx http-server

# またはブラウザで直接 sample.html を開く
open sample.html  # macOS
```

3. ブラウザで `http://localhost:8000` にアクセス

## プロジェクト情報の管理

### JSONファイルの構造

`public/projects/projects.json` に全プロジェクトの情報を一元管理。

#### 基本的なスキーマ

```json
{
  "projects": {
    "p1": {
      "title": "プロジェクト名",
      "shortTitle": "短縮名",
      "summary": "一行説明",
      "tags": ["エンジニア", "ビジネス", "社会福祉", "研究"],
      "overview": "プロジェクト概要",
      "why": "背景と課題",
      "what": "解決策と技術",
      "role": "役割と行動",
      "techStack": "Python, Django, React, AWS",
      "sections": [
        // セクション情報（下記参照）
      ]
    }
  }
}
```

### セクションタイプ

#### 1. `hero` - メイン画像セクション
ドロワーの先頭に大きく表示される画像
```json
{
  "type": "hero",
  "image": "/projects/pX/main.jpg",
  "alt": "画像の説明"
}
```

#### 2. `text` - テキストセクション
タイトルと本文を含むセクション
```json
{
  "type": "text",
  "title": "セクションタイトル",
  "content": "段落形式のテキスト内容"
}
```

#### 3. `image` - インライン画像セクション
キャプション付きの画像
```json
{
  "type": "image",
  "image": "/projects/pX/work.jpg",
  "caption": "画像の説明",
  "width": "full"  // "full"で全幅、省略で半幅
}
```

### 新規プロジェクトの追加手順

#### 1. ディレクトリと画像を準備
```bash
mkdir -p public/projects/pX  # pX = 新規プロジェクトID
cp /path/to/image1.jpg public/projects/pX/main.jpg
cp /path/to/image2.jpg public/projects/pX/detail.jpg
```

#### 2. `projects.json` に情報を追加
```json
"pX": {
  "title": "新規プロジェクト名",
  "shortTitle": "略称",
  "summary": "一行説明",
  "tags": ["エンジニア", "研究"],
  "overview": "詳しい概要",
  "why": "課題背景",
  "what": "実施した解決策",
  "role": "自分の役割",
  "techStack": "使用した技術",
  "sections": [
    {
      "type": "hero",
      "image": "/projects/pX/main.jpg",
      "alt": "メイン画像"
    },
    {
      "type": "text",
      "title": "プロジェクトの背景",
      "content": "プロジェクトの実施背景や課題について詳しく説明します。"
    },
    {
      "type": "image",
      "image": "/projects/pX/detail.jpg",
      "caption": "実装結果や成果物",
      "width": "full"
    }
  ]
}
```

#### 3. `sample.html` に基本情報を追加
```javascript
// projectsData 配列に追加
{ 
  id: 'pX', 
  title: '新規プロジェクト名', 
  shortTitle: '略称', 
  summary: '一行説明', 
  tags: ['エンジニア', '研究'] 
}
```

#### 4. （オプション）フィーチャープロジェクトに指定
`renderFeatured()` 関数の `featuredIds` に `'pX'` を追加

## カスタマイズガイド

### タグの色を変更

`sample.html` の `getTagColorClass()` 関数を編集：

```javascript
function getTagColorClass(tag) {
    switch(tag) {
        case 'エンジニア': return 'bg-indigo-50 text-indigo-700 border-indigo-200';
        case '社会福祉': return 'bg-teal-50 text-teal-700 border-teal-200';
        case 'ビジネス': return 'bg-amber-50 text-amber-700 border-amber-200';
        case '研究': return 'bg-purple-50 text-purple-700 border-purple-200';
    }
}
```

### フィーチャープロジェクトを変更

```javascript
// sample.html の renderFeatured() 関数内
const featuredIds = ['p1', 'p6', 'p15'];  // 変更したいプロジェクトID
```

### カオスマップの色を調整

```javascript
// sample.html の renderChaosMap() 関数内
const axesData = {
    '社会福祉': { color: 'bg-teal-500' },
    'エンジニア': { color: 'bg-indigo-500' },
    'ビジネス': { color: 'bg-amber-500' },
    '研究': { color: 'bg-purple-500' }
};
```

### 技術スキルの並び替え

技術スキルは自動的に星評価（★）の多い順に並び替えられます。
`projects.json` では順序を編集してください。

## デプロイ

### GitHub Pages での展開

`Settings` → `Pages` で以下のように設定：
- Source: `main` branch
- Folder: `/` (root)

## 機能説明

### フィルタリング
タグボタンをクリックして、特定の領域に関連するプロジェクトのみを表示

### プロジェクト詳細
プロジェクトカードをクリックしてドロワーを開き、詳細情報と画像を確認

### カオスマップ
4つの領域の交差を可視化し、複数分野に関わるプロジェクトを表示

### 技術スタック
プロジェクトごとに使用した技術スタックを表示

## トラブルシューティング

### 画像が表示されない
- `public/projects/pX/` ディレクトリが存在するか確認
- `projects.json` のパスが正しいか確認
- ブラウザのコンソール（F12）でエラーをチェック

### JSON が読み込まれない
- サーバー経由でアクセスしているか確認（ローカルファイル開きは不可）
- ブラウザの Network タブで `/projects/projects.json` が 200 を返しているか確認
- CORS エラーが出ていないか確認

### スタイルが反映されない
- ブラウザのキャッシュをクリア（Ctrl+Shift+R または Cmd+Shift+R）
- Tailwind CSS の CDN が正常に読み込まれているか確認

## バージョン履歴

### v2.0.0 (2026-05-25)
- JSON形式でのプロジェクト情報管理に統一
- セクション単位での柔軟な画像・テキスト配置
- 各プロジェクトのカスタムレイアウト対応
- カオスマップ座標の精密化
- 技術スキルの星評価による自動並び替え

### v1.0.0
- 基本的なポートフォリオサイトの完成