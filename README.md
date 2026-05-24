# RGB/HEX to Scratch Colors Converter

RGBまたはHEXからScratch Color（Scratch MIT対応）のコンバーターです。
Hue(1～100)、Saturation、Lightness に変換し、コピーペースト可能です。

## 🎨 機能

- **HEX入力**: HEXカラーコード（例: #FF5733）から変換
- **RGB入力**: RGB値（例: R=255, G=87, B=51）から変換
- **カラーピッカー**: ビジュアルにカラーを選択
- **複数出力形式**:
  - Hue (1～100)
  - Saturation (0～100)
  - Lightness (0～100)
  - Scratchコード (`set color effect to X`)
  - HEXカラーコード
  - RGBカラー

## 📋 使い方

1. 以下のいずれかの方法で色を指定:
   - **HEX入力タブ**: `#FF5733` または `FF5733` を入力
   - **RGB入力タブ**: R, G, B の値（0～255）を入力
   - **カラーピッカータブ**: 視覚的に色を選択

2. 「変換する」ボタンをクリック

3. 変換結果が表示されます。各値の横の「Copy」ボタンでクリップボードにコピー可能

## 🚀 クイックスタート

### ローカルで使う
```bash
# ブラウザで開く
open index.html
# または
start index.html
```

### オンラインで使う
GitHubからファイルをダウンロードしてブラウザで開くか、GitHub Pagesで公開できます。

## 📝 Scratch の色効果について

Scratchの色効果は以下のように機能します：

```scratch
set [color v] effect to (Hue値)
```

- **Hue（色相）**: 0～100（0が赤、50が青、100が赤に戻る）
- **Saturation（彩度）**: -100～100（-100が白、0が元色、100が純色）
- **Lightness（明度）**: -100～100（-100が黒、0が元色、100が白）

## 🛠️ 技術仕様

### 変換アルゴリズム

#### HEX → RGB
```javascript
// HEXコードの16進数を10進数に変換
R = HEX[0:2] → 10進数
G = HEX[2:4] → 10進数
B = HEX[4:6] → 10進数
```

#### RGB → HSL（Hue/Saturation/Lightness）
```javascript
// RGB（0-255）を正規化
r = R / 255
g = G / 255
b = B / 255

max = max(r, g, b)
min = min(r, g, b)

// Lightness（明度）の計算
L = (max + min) / 2

// Saturation（彩度）の計算
if L < 0.5:
    S = (max - min) / (max + min)
else:
    S = (max - min) / (2 - max - min)

// Hue（色相）の計算
if max == min:
    H = 0
elif max == r:
    H = 60 × (((g - b) / (max - min)) mod 6)
elif max == g:
    H = 60 × (((b - r) / (max - min)) + 2)
elif max == b:
    H = 60 × (((r - g) / (max - min)) + 4)

// Scratchフォーマット（0～100）に正規化
H_scratch = (H / 360) × 100
S_scratch = S × 100
L_scratch = L × 100
```

## 📦 ファイル構成

```
RGB.HEX2ScratchColors/
├── index.html          # メインのHTMLファイル（スタイル・スクリプト含む）
└── README.md          # このファイル
```

## 🎯 サポートされるフォーマット

### 入力
- ✅ HEX: `#RRGGBB`, `RRGGBB`, `#RGB`, `RGB`
- ✅ RGB: `R, G, B` (0-255)
- ✅ Color Picker: ブラウザのネイティブカラーピッカー

### 出力
- ✅ Hue (0-100)
- ✅ Saturation (0-100)
- ✅ Lightness (0-100)
- ✅ Scratch Code
- ✅ HEX Code
- ✅ RGB Format

## 🌐 ブラウザ互換性

- ✅ Chrome/Chromium
- ✅ Firefox
- ✅ Safari
- ✅ Edge
- ✅ モバイルブラウザ

## 📄 ライセンス

MITライセンス

## 🤝 貢献

バグ報告や改善提案は Issues で お願いします。

## 💡 使用例

### 例1: 赤色の変換

| 入力 | 出力 |
|------|------|
| HEX: `#FF0000` | Hue: `0` |
| RGB: `255, 0, 0` | Saturation: `100` |
| | Lightness: `50` |

### 例2: 青色の変換

| 入力 | 出力 |
|------|------|
| HEX: `#0000FF` | Hue: `67` |
| RGB: `0, 0, 255` | Saturation: `100` |
| | Lightness: `50` |

---

**Scratch MIT公式**: https://scratch.mit.edu/
