# 公众号图床（host5）

2026-08-29 新建，替代 `sangeng-ai-image-host`（该仓库已达 1.28 GB，git pull 频繁超时）。

## 硬性规则

1. **上传前必须压缩**：一律 `magick <src> -quality 92 -strip <dst>.jpg`，像素尺寸不变。
   实测水墨/水彩类插图 2.3 MB PNG → 0.3–0.6 MB JPEG，减 84%，无可见 artifacts。
   文字型图（法义图、开题卡）压缩后须重跑 OCR 校验，确认逐字一致。
2. **无损原件不进图床**：PNG 原件留在各项目工作区作审计原件。
3. 目录结构：`images/<账号>/<plan-id>/<角色>.jpg`
4. URL 按 commit SHA 固定引用：
   `https://cdn.jsdelivr.net/gh/lairulan/weishi-image-host@<commit_sha>/images/...`
5. 克隆用稀疏方式，避免重蹈全量克隆超时：
   ```
   git clone --filter=blob:none --no-checkout https://github.com/lairulan/weishi-image-host.git
   git sparse-checkout init --cone && git sparse-checkout set images/<账号>
   git checkout main
   ```

## 旧仓库

`sangeng-ai-image-host` 冻结为只读，**不得重写历史**：所有已发布文章的图片 URL 都按旧 commit SHA 引用，
重写历史会让本生宝鬘 101 篇、唯识 14 篇、三更AI 十余篇的配图全部 404。
