# qf · data model

version: 0.1
last-updated: 2026-07-28

## SoT

**repo 內不存在任何業務資料。** 資料只活在使用端瀏覽器 `localStorage`，由使用者自行匯入。
這是本專案與 08-single-page-tool 的 `data.js` 慣例的差異點：資料 = 個資（PD+FC T0/T1），
禁止進版控 / 禁止上線，故 SoT 移到裝置端。頁面是純 view + localStorage adapter。

## localStorage

| key | 內容 |
|---|---|
| `qf.items.v1` | `Item[]` 的 JSON 字串 |

## Item

```
{ group: string, label: string, value: string }
```

- `group`：顯示分組（如 profile / links / ja）。lowercase。
- `label`：欄名，原樣顯示（可為日文欄名如「現住所」）。
- `value`：字串。可含換行（長文）。
- 去重鍵：`(group, label)`。重複匯入 = 覆寫 value。
- 順序：append-only，依匯入順序渲染（同組相鄰）。

## 匯入（kiln/mark 式：點擊即選檔上傳 .json，無對話框）

`import` 鈕 → 系統選檔器 → 讀檔合併。格式兩種：

1. 扁平物件 `{"欄名":"值", ...}` — group = 檔名去掉 `.json` 與 `seed` 尾綴
   （`qf_seed.json` → `qf`；`links.json` → `links`）。與 form-copilot snapshot 直接相容。
2. 陣列 `[{group, label, value}, ...]` — 即 export 的原樣格式，round-trip 用（內嵌 group 優先）。

非字串 value 轉字串；空值丟棄。手機流程：AirDrop/儲存 seed 到「檔案」→ import 選之。

## Schema 變更規則

改 Item 欄位 = bump localStorage key 版本（`qf.items.v2`）+ 本檔同步 + migration 一段。
UI 變更不准動 schema（08 spec 規則 3）。

## 種子

`DungeonsRoot/PD+FC/Personal-Directory/human/quick_fill/qf_seed.json`（私庫，勿混入本 repo）。
