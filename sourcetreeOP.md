# SourceTree 操作步驟文件

---

## 前置準備

1. 開啟 **SourceTree**。
2. 點選上方工具列 **「New」→「Create Local Repository」**。
3. 選擇目的地路徑（例如 `C:\Java_Framework\ai_skills\sourcetree-demo`），輸入名稱後按 **「Create」**。
4. SourceTree 開啟該 Repository 的主畫面。

---

## 加入 README.md 檔案

1. 在 `sourcetree-demo` 資料夾中手動新增 `README.md` 檔案（使用文字編輯器或檔案總管）。
2. 回到 SourceTree，左側點選 **「File Status」**（或上方 **「Uncommitted changes」**）。
3. 在 **「Unstaged files」** 區域看到 `README.md`，勾選左側核取方塊將其移至 **「Staged files」**。
4. 在下方 **「Commit message」** 欄輸入：`加入 README.md`。
5. 按右下角 **「Commit」** 按鈕完成提交。

---

## 加入 Branch yahoo-v1

1. 在上方工具列點選 **「Branch」** 按鈕。
2. 在 **「New Branch」** 對話框輸入分支名稱：`yahoo-v1`。
3. 確認 **「Checkout New Branch」** 核取方塊已勾選。
4. 按 **「Create Branch」**，SourceTree 會自動切換到 `yahoo-v1` 分支。

### Branch yahoo-v1 加入檔案 A1.txt

1. 在 `sourcetree-demo` 資料夾中手動新增 `A1.txt` 檔案。
2. 回到 SourceTree，**「File Status」** 頁籤顯示 `A1.txt` 在 Unstaged 區域。
3. 勾選 `A1.txt` 移至 **「Staged files」**。
4. 輸入 Commit message：`加入 A1.txt`。
5. 按 **「Commit」**。

---

## 加入 Branch seednet-v1

1. 先切換回 `master`：在左側 **「BRANCHES」** 清單中，雙擊 **`master`** 切換過去。
2. 在上方工具列點選 **「Branch」** 按鈕。
3. 輸入分支名稱：`seednet-v1`。
4. 確認 **「Checkout New Branch」** 已勾選，按 **「Create Branch」**。

### Branch seednet-v1 加入檔案 A2.txt

1. 在 `sourcetree-demo` 資料夾中手動新增 `A2.txt` 檔案。
2. 回到 SourceTree，**「File Status」** 顯示 `A2.txt` 在 Unstaged 區域。
3. 勾選 `A2.txt` 移至 **「Staged files」**。
4. 輸入 Commit message：`加入 A2.txt`。
5. 按 **「Commit」**。

### Branch seednet-v1 加入檔案 A3.txt

1. 在 `sourcetree-demo` 資料夾中手動新增 `A3.txt` 檔案。
2. 回到 SourceTree，**「File Status」** 顯示 `A3.txt` 在 Unstaged 區域。
3. 勾選 `A3.txt` 移至 **「Staged files」**。
4. 輸入 Commit message：`加入 A3.txt`。
5. 按 **「Commit」**。

---

## Rebase Branch seednet-v1 到 yahoo-v1

> 目的：將 `seednet-v1` 的 commit（A2.txt、A3.txt）接到 `yahoo-v1` 的最新 commit 之後。

1. 確認目前位於 **`seednet-v1`** 分支（左側 BRANCHES 清單中該分支名稱為粗體）。
   - 若不是，雙擊 `seednet-v1` 切換過去。
2. 在上方工具列點選 **「Repository」→「Rebase...」**（部分版本在 **「Actions」** 選單）。
3. 在 Rebase 對話框的 **「Rebase current branch onto:」** 下拉選單中選擇 **`yahoo-v1`**。
4. 按 **「OK」** 執行 Rebase。
5. Rebase 完成後，左側 **「History」** 圖形視圖會顯示線性提交記錄：

```
●  加入 A3.txt       ← seednet-v1 (HEAD)
●  加入 A2.txt
●  加入 A1.txt       ← yahoo-v1
●  加入 README.md    ← master
```

---

## 最終 Branch 結構說明

| 分支 | 包含檔案 |
|------|---------|
| `master` | README.md |
| `yahoo-v1` | README.md、A1.txt |
| `seednet-v1`（rebase 後） | README.md、A1.txt、A2.txt、A3.txt |

