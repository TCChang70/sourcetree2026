# 業界標準 Git Flow：SourceTree 三角色協作實戰演練

本文件透過模擬 3 個不同角色的日常工作，詳細拆解業界標準的 **Git Flow** 協作模式。所有操作皆以 **SourceTree** 的圖形化介面（GUI）為操作基準，涵蓋 `fetch`、`pull`、`branch`、`commit`、`push` 與 `Pull Request (PR)` 的完整生命週期。

---

## 👥 角色與職責設定

| 角色 | 姓名 | 標籤 | 主要職責與負責分支 |
|------|------|------|-------------------|
| 👑 **專案負責人 (Lead)** | **Alice** | `Alice` | 負責專案初始化、發布管理、PR 代碼審查。操作 `main`、`develop`、`release` 分支。 |
| 💻 **前端工程師 (Dev A)** | **Bob** | `Bob` | 負責開發新功能。操作 `feature/*` 分支。 |
| 🛠️ **後端/維運工程師 (Dev B)** | **Charlie**| `Charlie` | 負責緊急修復與一般錯誤排除。操作 `hotfix/*` 或 `bugfix/*` 分支。 |

---

## 🌳 Git Flow 核心分支架構回顧

- `main`：正式上線版本，必須永遠保持穩定。
- `develop`：主要開發分支，所有新功能整合於此。
- `feature/*`：從 `develop` 切出，開發新功能，完成後合併回 `develop`。
- `hotfix/*`：從 `main` 切出，修復線上緊急 Bug，完成後合併回 `main` 與 `develop`。
- `release/*`：從 `develop` 切出，準備發布新版本，完成後合併回 `main` 與 `develop`。

---

## 🎬 實戰情境模擬

### 階段一：專案初始化設定 👑 `Alice`
Alice 作為負責人，需要建立基礎開發環境。

1. **Clone 專案與初始化分支**
   - 透過 SourceTree 點擊 **Clone**，輸入遠端數據庫網址。
   - 預設位於 `main` 分支。
2. **建立 `develop` 分支**
   - **Branch (分支)**：點擊上方工具列的 **Branch**，新分支命名為 `develop`，勾選「Checkout new branch」。
3. **推送到遠端 (Push)**
   - **Push (推送)**：點擊上方工具列的 **Push**，勾選 `develop` 分支，推送到遠端伺服器（Origin）。
4. **設定保護分支 (在 GitHub/GitLab 網頁端)**
   - Alice 進入網頁端，將 `main` 與 `develop` 設定為保護分支，要求必須透過 **Pull Request (PR)** 才能合併。

---

### 階段二：新功能開發 💻 `Bob`
Bob 收到任務，需要開發「會員登入」功能。

1. **獲取最新狀態 (Fetch & Pull)**
   - **Fetch (擷取)**：點擊上方工具列的 **Fetch**，確認遠端是否有更新。
   - **切換分支**：在左側側邊欄雙擊 `develop` 切換過去。
   - **Pull (拉取)**：點擊上方工具列的 **Pull**，將最新的 `develop` 同步到本地。
2. **建立 Feature 分支**
   - **Branch**：確保目前在 `develop`，點擊 **Branch**，命名為 `feature/login`。
3. **撰寫程式與提交 (Commit)**
   - Bob 新增了 `login.html` 與 `login.js`。
   - 回到 SourceTree，在「Unstaged files (未暫存檔案)」勾選剛修改的檔案（移至 Staged files）。
   - **Commit**：點擊左上角 **Commit**，輸入訊息 `feat: add user login page`，點擊右下角 Commit 按鈕。
4. **推送到遠端 (Push)**
   - **Push**：點擊 Push 工具，勾選 `feature/login`，點擊確推送。
5. **建立 Pull Request (PR)**
   - 在 SourceTree 左側側邊欄針對 `feature/login` 按右鍵，選擇 **Create Pull Request**（將開啟瀏覽器）。
   - 設定來源為 `feature/login`，目標為 `develop`。
   - 提交 PR，等待 Alice 審查。

---

### 階段三：線上緊急 Bug 修復 🛠️ `Charlie`
此時，線上系統（`main` 分支）發生了導致系統崩潰的問題，Charlie 需要緊急介入。

1. **獲取最新狀態 (Fetch)**
   - **Fetch**：Charlie 點擊 **Fetch**，獲取遠端所有分支狀態。
2. **建立 Hotfix 分支 (直接從 main 切出)**
   - **切換分支**：雙擊左側的 `main` 分支。
   - **Pull**：點擊 **Pull** 確保擁有最新的正式版代碼。
   - **Branch**：確保在 `main`，點擊 **Branch**，命名為 `hotfix/crash-fix`。
3. **修復 Bug 與提交 (Commit)**
   - Charlie 修復了崩潰問題。
   - 暫存檔案 -> 點擊 **Commit**，輸入訊息 `fix: resolve system crash issue`。
4. **推送到遠端 (Push)**
   - **Push**：點擊 推送，勾選 `hotfix/crash-fix`。
5. **建立雙向 Pull Request (PR)**
   - Hotfix 必須同時合併回 `main` 與 `develop`。
   - Charlie 開啟網頁端：
     - 建立 PR 1：`hotfix/crash-fix` -> `main`
     - 建立 PR 2：`hotfix/crash-fix` -> `develop`

---

### 階段四：代碼審查與衝突處理 👑 `Alice` 與 💻 `Bob`

**第一步：處理緊急的 Hotfix (Alice)**
1. Alice 收到 Charlie 的 PR 通知。
2. 透過網頁端審查代碼，確認無誤後，**Approve (核准)** 並 **Merge (合併)** 回 `main` 與 `develop`。
3. （可選）Alice 透過 SourceTree 在 `main` 的合併節點上按右鍵選擇 **Tag**，打上 `v1.0.1` 標籤並 Push Tags。

**第二步：處理 Bob 的新功能並解決衝突 (Alice & Bob)**
1. Alice 審查 Bob 的 `feature/login` PR，發現因為 Charlie 剛剛合併了 `hotfix` 到 `develop`，Bob 的 PR 出現了**合併衝突 (Merge Conflict)**。
2. 👑 Alice 退回 PR，請 Bob 解決衝突。
3. 💻 **Bob 解決衝突的標準步驟：**
   - 在 SourceTree 點擊 **Fetch**。
   - 雙擊 `develop` 分支，點擊 **Pull**，更新到剛合併了 hotfix 的狀態。
   - 雙擊回到自己的 `feature/login` 分支。
   - 在 `develop` 分支上按 **右鍵 -> Merge develop into feature/login**。
   - 系統提示發生衝突 (Conflicts)。
   - Bob 開啟 VS Code 或編輯器，保留正確的程式碼（解決衝突）。
   - 回到 SourceTree，將解決衝突的檔案打勾 (Stage)。
   - 點擊 **Commit**，保留預設的合併訊息 `Merge branch 'develop' into feature/login`。
   - 點擊 **Push**，將解決衝突後的分支推送到遠端。
4. 👑 **Alice 最終合併：**
   - 網頁端 PR 會自動更新並顯示「無衝突 (No conflicts)」。
   - Alice 點擊 **Merge**，將 `feature/login` 合併至 `develop`。

---

### 階段五：完成與清理工作

1. **刪除遠端 Feature / Hotfix 分支**
   - 在網頁端 PR 合併後，Alice 或系統會自動刪除遠端的 `feature/login` 與 `hotfix/crash-fix`。
2. **清理本地分支 (Bob 與 Charlie)**
   - Bob 在 SourceTree 點擊 **Fetch**（勾選 Prune/修剪 遠端已刪除的分支）。
   - 切換回 `develop` 分支，點擊 **Pull** 取得最新代碼。
   - 在本地的 `feature/login` 上按右鍵 -> **Delete feature/login**，保持本地環境整潔。
   Charlie 亦同理刪除本地的 `hotfix/crash-fix` 分支。

---

## 💡 總結：SourceTree 操作關鍵心法

1. **先 Fetch 再做任何事**：開工前、合併前，養成隨手點擊工具列 `Fetch` 的好習慣。
2. **Push 之前考慮 Pull**：在推送到遠端前，若別人有更新，你的 Push 會被拒絕。請先 Pull（或 Pull 搭配 Rebase）。
3. **GUI 衝突解決**：發生衝突時，SourceTree 的 "Unstaged files" 區會顯示帶有橘色三角形 `!` 的檔案。使用外部編輯器修改後，加回 Staged 區即代表衝突已解決。
4. **Pull Request 是團隊溝通的橋樑**：所有的合併（Main、Develop）都應強制透過 PR，避免直接 Push 破壞核心分支的穩定性。