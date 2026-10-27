# aiapi-customizations — release assets

這個 repo 只放 Aiapi DSH 插件的發佈檔，供插件「檢查更新／立即更新」讀取。

```
index.json            # 最新版本的索引（插件讀這個）
latest.tgz            # 最新版本的安裝包（固定檔名）
<version>/            # 每個版本的原始檔（留存用）
```

## 使用方式（二選一）

**A. GitHub Pages（推薦，走 CDN、可控制快取）**

1. Settings → Pages → Source: `Deploy from a branch` → branch `main`、目錄 `/ (root)`
2. 網址：`https://<owner>.github.io/<repo>/index.json`

**B. GitHub raw（零設定）**

`https://raw.githubusercontent.com/<owner>/<repo>/main/index.json`

## 客戶端設定

在 DSH profile 的 `cordis.patch.yml`：

```yaml
- id: aiapi-customizations
  name: '@aiapi/dsh-customizations'
  config:
    updateManifestUrl: https://<owner>.github.io/<repo>/index.json
```

插件頁 → 檢查更新 → 立即更新。舊版機器用 `update-plugin.sh`。

## 發佈新版本

在 `desktop-shell/plugins/`：

```bash
node release.mjs --notes "…"
OUT_DIR=<this repo> bash publish-cloud.sh --dir release/<版本> --provider github-raw --repo <owner>/<repo> --no-verify
cd <this repo> && git add -A && git commit -m "release <版本>" && git push
```
