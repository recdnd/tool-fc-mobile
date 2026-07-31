# fc-mobile · design spec

version: 0.3
last-updated: 2026-07-29
mode: **無**（不套 8 桌面模式；Rec 裁定 2026-07-29）

## 勘誤（0.1 的錯誤）

初版引用 01 Lab Instrument 作為模式對象——**引用錯誤**：kiln／Ruvia 等模式是為桌面
滑鼠交互設計的（hover 反白、1px 密集邊界、ambient 顯隱）。fc-mobile 是純手機工具，
按鈕與回饋必須走移動端邏輯。桌面版已於 0.2 撤銷，僅存手機單版。

## 對齊對象（0.3 起）

**pf-rec mobile 版**是唯一設計參照：palette `--accent:#dc2626`、`--btn-bg:rgba(0,0,0,.1)`；
操作鈕 = 44px 半透明圓鈕＋backdrop blur，右下角固定列；`:active` = scale(0.95)＋accent 底白字；
列項回饋 = 文字轉 accent（**絕不反白變黑**——那是 kiln 桌面殘留，已於 0.3 清除）；
無頂部 bar、無 filter bar，status 為浮動小字。

## 適用規則

依 `derivatives/design-spec/ANTI_PATTERNS.md` 之 mobile 條（27–33）＋共通基底：

- 觸控目標 ≥ 44px（列高 44、頂鈕 40 見方）；回饋走 `:active` 反白＋`navigator.vibrate(20–50ms)`，無 hover 依賴。
- `100dvh`、`env(safe-area-inset-*)`、`viewport-fit=cover`、touch listener `passive: true`。
- 白底黑墨、Courier、字重 400、紅只作 status 警示；無圓角、無陰影、無 transition。
- 極簡到底：無 brand、無 crumb、無教學文案；空庫＝整片 📃 即 import 入口。
- 訊息第三人稱被動 3 秒自清；clear 二段確認不用 confirm()。

## 禁止回歸項

- 不加桌面版、不做 responsive 分支——手機單版就是全部。
- 不引用任何桌面模式 spec 作為視覺依據。
- repo（PD+FC 私庫內）與頁面本身永不內嵌個資；資料只在裝置 localStorage。
