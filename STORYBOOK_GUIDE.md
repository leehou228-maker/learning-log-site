# 🎨 幼兒有聲書 Demo 完整指南

## 📚 Demo 預覽

**線上版本**：https://leehou228-maker.github.io/learning-log-site/storybook_demo.html

**故事名稱**：《小兔子的森林冒險》
**頁數**：10 頁
**適合年齡**：3-6 歲
**教育意義**：友情、分享、探索

---

## 🎯 Demo 功能特色

✅ **互動式翻頁** - 點擊按鈕切換頁面
✅ **自動配音** - 使用 Web Speech API 自動朗讀（支持粵語）
✅ **精美插圖** - 使用 Unsplash 高質素圖片
✅ **響應式設計** - 手機、平板、電腦都適用
✅ **完全免費** - 無需任何付費工具

---

## 🔧 如何使用這個 Demo

### 方法 1：直接使用（最簡單）

1. 打開瀏覽器訪問：
   ```
   https://leehou228-maker.github.io/learning-log-site/storybook_demo.html
   ```

2. 點擊「🔊 播放配音」聽故事

3. 點擊「下一頁」繼續故事

4. 陪同孩子一起觀看！

---

### 方法 2：下載到自己電腦（可離線使用）

1. **下載文件**
   ```bash
   # 在終端機執行
   cd ~/Desktop
   curl -O https://leehou228-maker.github.io/learning-log-site/storybook_demo.html
   ```

2. **打開文件**
   - 雙擊 `storybook_demo.html`
   - 會在預設瀏覽器中打開
   - 可以離線使用！

---

### 方法 3：自定義故事（進階）

#### 步驟 1：修改故事文本

打開 `storybook_demo.html` 文件，找到 `pageTexts` 部分：

```javascript
const pageTexts = {
    1: "你的故事內容...",
    2: "你的故事內容...",
    // ...
};
```

修改為你自己的故事！

#### 步驟 2：更換圖片

找到 `<img src="...">` 部分，替換為你的圖片：

```html
<!-- 原本的 Unsplash 圖片 -->
<img src="https://images.unsplash.com/..." class="page-image">

<!-- 替換為你的圖片 -->
<img src="your-image.jpg" class="page-image">
```

**建議圖片尺寸**：800 x 600 像素

---

## 🎨 如何用 AI 創建更專業版本

### 步驟 1：用 ChatGPT 創作故事

**Prompt 模板**：
```
你是一位專業的兒童故事作家。請創作一個適合3-6歲兒童的故事。

要求：
1. 字數：每頁 50-80 字
2. 總頁數：10 頁
3. 語言：粵語（廣東話）
4. 主題：友情與分享
5. 角色設定：小兔子白白、小鳥吱吱、小松鼠毛毛

輸出格式：
【第1頁】
文本：...

【第2頁】
文本：...

（依此類推）
```

### 步驟 2：用 Midjourney 生成插圖

**Prompt 範例**（第1頁 - 可愛的小兔子）：
```
/imagine cute white rabbit with long ears, fluffy tail,
standing in a magical forest, children book illustration style,
soft pastel colors, whimsical, friendly, watercolor --ar 4:3 --v 6 --style raw
```

**Prompt 範例**（第3頁 - 小鳥朋友）：
```
/imagine cute small bird singing on a tree branch,
children book illustration, soft colors, friendly expression,
storybook style, watercolor --ar 4:3 --v 6
```

**保存圖片**：
- 下載生成的圖片
- 重命名為 `page1.jpg`, `page2.jpg`, ...
- 放在同一個文件夾

### 步驟 3：用 ElevenLabs 錄製配音

1. **註冊帳號**
   - 訪問：https://elevenlabs.io
   - 免費計劃：每月 10,000 字符

2. **選擇聲音**
   - 推薦：Bella（溫柔女聲）或 Adam（溫和男聲）

3. **錄製每一頁**
   ```
   文本：「從前從前，有一隻可愛的小兔子...」
   調整：
   - Stability: 75%
   - Similarity: 85%
   - Style: 中等
   ```

4. **下載音頻**
   - 格式：MP3
   - 重命名：`audio1.mp3`, `audio2.mp3`, ...

### 步驟 4：整合到 HTML

替換 Web Speech API 為真實音頻：

```html
<!-- 在 <head> 中添加 -->
<audio id="audio1" src="audio1.mp3"></audio>
<audio id="audio2" src="audio2.mp3"></audio>
<!-- ... -->

<!-- 修改 JavaScript -->
function startSpeech() {
    const audio = document.getElementById(`audio${currentPage}`);
    audio.play();
}
```

---

## 📊 成本估算

### 方案 A：完全免費
- ChatGPT 免費版
- Unsplash 圖片
- Web Speech API 配音
- **總成本：$0**

### 方案 B：半專業
- ChatGPT Plus：$20/月
- Midjourney Basic：$10/月
- ElevenLabs Free：$0/月
- **總成本：$30/月**

### 方案 C：專業級
- ChatGPT Plus：$20/月
- Midjourney Standard：$30/月
- ElevenLabs Starter：$5/月
- **總成本：$55/月**

---

## 🚀 進階功能建議

### 1. 添加背景音樂
```html
<audio id="bgMusic" loop>
    <source src="gentle-music.mp3" type="audio/mpeg">
</audio>
```

### 2. 添加翻頁動畫
```css
.page {
    transition: transform 0.6s ease-in-out;
}

.page.turning {
    transform: rotateY(-90deg);
}
```

### 3. 添加自動播放模式
```javascript
let autoPlay = false;

function toggleAutoPlay() {
    autoPlay = !autoPlay;
    if (autoPlay) {
        playNextPage();
    }
}

function playNextPage() {
    if (autoPlay && currentPage < totalPages) {
        startSpeech();
        setTimeout(() => {
            nextPage();
            playNextPage();
        }, 10000); // 10 秒後自動翻頁
    }
}
```

### 4. 添加下載功能
```javascript
function downloadAsPDF() {
    // 使用 jsPDF 庫將網頁轉換為 PDF
    const doc = new jsPDF();
    // ... 實現代碼
}
```

---

## 📱 部署到網絡

### 選項 1：GitHub Pages（免費）
1. 創建 GitHub 帳號
2. 創建新 Repository
3. 上傳 `storybook_demo.html`
4. 啟用 GitHub Pages
5. 分享你的連結！

### 選項 2：Netlify（免費）
1. 訪問 https://netlify.com
2. 拖放文件夾
3. 獲得免費域名
4. 分享！

---

## 🎓 教育應用建議

### 在家使用
- 睡前故事時間
- 親子共讀
- 學習粵語

### 在學校使用
- 幼兒園課堂活動
- 語言學習教材
- 創意寫作啟發

### 在線教學
- Zoom 分享屏幕
- 錄製為影片上傳 YouTube
- 製成互動課件

---

## 📞 需要幫助？

如果你想要：
- 🎨 **更多主題的故事**（動物、太空、恐龍等）
- 🌍 **不同語言版本**（普通話、英語等）
- 🎵 **添加背景音樂和音效**
- 📱 **製作成手機 App**
- 🎬 **製作成 YouTube 影片**

隨時聯絡我！我係葡撻哈哈 AI 🥧

---

## 📄 完整源代碼下載

所有文件都已開源，你可以自由使用、修改和分享！

**GitHub Repository**：
https://github.com/leehou228-maker/learning-log-site

---

**製作日期**：2026-03-13
**製作人**：葡撻哈哈 AI 🥧
**版本**：1.0
