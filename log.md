# Demo Page Version Log

## 2026-09-16

- Version: initial
- Description: 依 `github_demo/nelvc_demo` 的版面建立 ETN-elwavlm（EL-WavLM）demo 頁
  - `index.html` 由 `build_index.py` 產生（12 組試聽、12 張頻譜圖是程式產生的，不手打檔名）
  - 表格 Table 1／2／3 的數字與粗體逐格照抄 `ICASSP2027_elw/main.tex` 的
    `tab:main`／`tab:curriculum`／`tab:loss`，沒有重算或補充草稿以外的數字
  - 圖檔／音檔來源：`espnet/egs/tmhint/etn_baseline/downloads/ICASSP2027_elw/`
    （t-SNE 用 `_s3` 版、Fig. 1 用 f3 版，與論文現行採用的版本相同）
  - 模型範圍：試聽區只放論文 Table 1 的三個系統（ETN-mel／ETN-wavlm／ETN-elwavlm）
    ＋論文正文自己引用的兩個參考錄音（未處理 PEL、NL 真值）；
    `elw_a2`（Stage 3-3 only）音檔已從 `audio/` 移除

## TODO

- [ ] 論文定稿後同步 abstract 與表格數字
- [ ] 確認是否加入 GitHub Pages 設定（目前只有靜態檔，尚未 git init）
- [x] 每句中文 transcript 已補上（來源 `downloads/tmhint.txt`，行號＝句號 1–320；已與 `data/NL07v4_eval/text` 的音素標註核對過）
