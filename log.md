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

- Version: 2026-09-16b
- Description: 每個 sample 卡片補上該句的 t-SNE（頻譜圖下方、試聽上方）
  - 六張新圖（NL07／NL08 × 句 284／304／318）用
    `fig_tsne_frame.py --s3 --stage plot-utt --trg <TRG> --utt <TRG>_<句號>` 產生，
    與論文 Fig. 2 同一套規則：encoder 空間、after-Stage-3 checkpoint、
    三格（ETN-elwavlm-frozen／Stage 3-3 only／Full schedule），沒有超出論文比較範圍
  - 一張圖含兩位病人（上 PEL03、下 PEL11），所以同一目標語者的兩張卡片共用同一張圖，
    圖說註明這張卡片是哪一列
  - `fig_tsne_frame.py` 這次補的是既有 `--s3` 旗標在單句版沒接上的部分：
    單句版現在也只畫 encoder、檔名加 `_s3`、stats 另存 `fig3_frame_stats_utt_<TRG>_s3.json`
    （原本單句 stats 檔名不帶 TRG，換目標語者會靜靜覆蓋）；不帶 `--s3` 的舊行為未改動
- Description: git 歷史移除 Claude co-author 署名（`git filter-branch --msg-filter`，
  三個 commit 重寫後 force push；檔案內容未變）

## TODO

- [ ] 論文定稿後同步 abstract 與表格數字
- [ ] 確認是否加入 GitHub Pages 設定（目前只有靜態檔，尚未 git init）
- [x] 每句中文 transcript 已補上（來源 `downloads/tmhint.txt`，行號＝句號 1–320；已與 `data/NL07v4_eval/text` 的音素標註核對過）

## 2026-09-16 例句 284 → 287

- Why: 頻譜圖 PEL03 句 284 的未轉換 EL W-CER 0.5 低於三個系統（0.6–0.8）。查 `obj_eval` 屬實：
  Whisper 對這句原始 EL 恰好猜對一半，是 40 句中唯一「原始比三系統都低」的離群句，不是計算錯誤。
- What: 例句改為 287（那個牆上掛著一幅油畫；PEL03→NL07 原始 1.0／ETN-mel 1.0／ETN-wavlm 0.9／ETN-elwavlm 0.2）。
  `build_index.UTTS` 改 287/304/318；重產 4 張頻譜圖、18 個音檔、單句 t-SNE（after-Stage-3 版）
  補齊 NL08 的三句（先前只有 NL07），284 素材全部移除。
- Note: PEL11→NL07 句 287 三系統皆 0.9，該卡片對比不明顯；PEL11→NL08 為 0.9／0.9／0.5。
- Description: 主程式 `result_csv/tools/paper/export_plot_pkg.py` 的 UTTS 同步改為 (318,304,287)。
