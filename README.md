# 魔法識字卡

離線可用嘅識字卡小程式（index.html 單一檔案）。

打開：https://sky3d20-jpg.github.io/magic-cards/

## 聲音
- `audio/`：265 張內置卡嘅廣東話錄音，用 Microsoft zh-HK-HiuMaanNeural 預先生成。格式係 mp3、24kHz、單聲道、40kbps。
  - `c_<unicode>.mp3`：字，停一停，再讀詞語
  - `s_`：單字
  - `w_`：詞語
  - `p_XX`：固定句子（指示、稀有卡名）
- `audio/manifest.json` 列出所有檔案。app 會先播錄音；搵唔到檔案、用 file:// 打開、或者家長自己加嘅字，就改用裝置嘅廣東話朗讀（speechSynthesis）。
- 多音字已經按字典讀音修正，詳情見 POLYPHONE_REPORT。
