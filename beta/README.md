# 魔法識字卡 測試版 (beta)

Served at `https://sky3d20-jpg.github.io/magic-cards/beta/`. Built on top of the 句子魔法 build
(main index sha256 `ddcc7ad2…`). The main app files (root `index.html`, root `audio/`) are untouched.

## Storage separation (important)
- The beta stores everything under the localStorage key **`magicCardsBetaV1`**.
- The main app's key **`magicCardsV1`** is only ever *read* (when you choose 「複製正式版進度嚟試」). The beta never writes or removes it.
- On first open you choose to copy the real progress (a read-only snapshot) or start fresh. You can copy again later from 家長 → 測試版設定.
- The beta never deletes any Cache Storage. It reuses the shared voice cache for `../audio/` and keeps its own clips in the `mc-beta-b1` cache.

## Files
- `index.html`: the single-file app. It bundles Hanzi Writer 3.7.3.
- `strokes.json`: stroke outlines, medians and radical-stroke indices for 255 characters. It is loaded lazily, cached, and never fetched from a CDN.
- `audio/b_01…b_66.mp3`: 66 new Cantonese clips (edge-tts zh-HK-HiuMaanNeural). All other speech reuses `../audio/` through `../audio/manifest.json`.
- `licenses/`: the third-party licence texts.

## Features
1. **部首魔法**: 3–4 known characters share a radical, which is highlighted in pink. The round asks 「估下同咩有關？」 with 3 picture choices, then 「邊個字有X？」, then a 拆字砌字 question (e.g. 日+月=明). There are 19 radical families built from the 265-card dictionary, and captured characters are preferred. The game unlocks once ≥2 captured characters share a radical, or when the parent toggle 「開放全部練習」 is on.
2. **描字＋筆順**: plays the stroke-order animation, then she traces stroke by stroke with gentle hints (each character can be traced at most twice). Entry points are the 「✍️ 描字」 button on album cards and an optional step after capture (on by default; parent toggle). Characters without stroke data use free tracing over a faint glyph. Free tracing passes at ≥65% coverage, with ≥45% in every 3×3 region that contains part of the glyph, and painting outside the glyph no more than 1.3× the painting inside it.
3. **親子時間**: 2–3 cards for the parent to read aloud: a chat/prediction question, 砌詞 with a tappable 「睇吓例子」 reveal, and 一齊讀 using the sentence. Each card has a 3P tip (停一停、提示、讚賞). There is no scoring; 「完成」 gives one family star per day.

## Stroke data coverage
- 246 of the 265 dictionary characters have stroke-order data. Separately, 9 component/combo characters are also in strokes.json.
- The 19 characters that use free tracing are: 吃抱摘搭圓乖田鴨兔蟲窗糖真猴虎蛇雀蝶粥
- Caveat: AnimCJK's zh-Hant forms follow the Taiwan standard (教育部標準字體). In a minority of components (for example some 辶 / 言 forms) they differ slightly from the HK 常用字字形表. Spot-check before relying on them for handwriting.

## Third-party licences
- **Hanzi Writer** 3.7.3, © 2014 David Chanin, MIT License. See `licenses/HanziWriter-LICENSE.txt`.
- **AnimCJK** (graphicsZhHant data, converted into `strokes.json`), © 2016-2026 FM&SH, https://github.com/parsimonhi/animCJK.
  - The glyph graphics derive from the Arphic PL KaitiM fonts and are distributed under the **Arphic Public License**: `licenses/AnimCJK-ARPHICPL.txt` (and the zh_TW text).
  - Other AnimCJK data is under the LGPL: `licenses/AnimCJK-LGPL.txt`.
  - See also `licenses/AnimCJK-COPYING.txt`.
  - Modification notice: the data was converted to JSON, and per-character radical stroke indices were added. No glyph shapes were altered.
