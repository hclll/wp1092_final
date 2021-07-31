# [109-2] Web Programming Final
## (Group 57) Chat Chat Chat

### Demo 影片連結

### 服務內容

* 能提供使用聊天室的聊天服務。
* 未註冊的使用這可以先註冊帳號，註冊完並登入後會進入主頁面。
* 主頁面顯示了使用者之前所加入的所有聊天室以及朋友。
* 使用者可以選擇創建聊天室或者加入已創立的聊天室。
* 進入聊天室後可以發送訊息，所有聊天室成員都能看見你所發的訊息。
* 可在設定頁面中設定頭像、個人訊息及更改密碼。

### Deployed 連結


### 使用之框架/模組/原始碼

#### 前端
* React
* React-Router ([ref](https://reactrouter.com/))
* Material-UI

#### 後端
* node.js
* Express
* Mongoose (後端接 mongodb)
* socket.io

### 心得

* 何承勳

```
這次的期末報告讓我學報了一些新的技術及知識，包括
1. Material-UI 的 css 框架。
2. Express 的一些之前沒用過的 middleware，如 multer（處理 `multipart/form-data` 的 middleware）
3. 用到一些 Mongodb 一些之前沒注意到的 operator，如 $push，$pull，以及 $pullAll 等
4. 發現與學會了 socket.io 的 room 功能。
5. Type checking 很重要。（我覺得我4b4應該要去學 typescript 了 இдஇ  ）
透過這次的報告，我學會了在團隊開發時的一些溝通能力以及互動方式，例如如何和組員分配工作，如何互助除錯，註解要寫的夠清楚等等，這些知識技巧是獨自寫程式時無法習得的，也是我認為我自己相當弱的一部分。另外，我認為雖然透過本課程能學習到最前衛的全端知識，但學海無涯，仍有需多未接觸以及未解決的問題等著我們學習。例如前端的UI及UX設計（本人相當沒有美感இдஇ）以及後端的諸多資安問題等等，皆是我自認為不足的地方。希望未來的幾年能將這些知識補足。
```

* 施冠宇

```
這次的期末專題，算是我第一次從無到有，做出一個完整的網路服務 project。相較於課程中的作業只需要寫部分的code，這次的 project 需要我們自己建立前後端的架構，對我來說是不小的挑戰，但同時也提供我們自由發揮的空間。過程中，最大的收穫不僅僅是對前後端有進一步的了解，更多的是透過團隊合作，學習到許多獨自寫程式無法習得的知識，而和組員討論的過程中，也能更有效發現問題並找到解決方案。此外，經由這次專題，我學到許多課程沒有教到的前後端設計，也發現許多之前不知道的套件和用法，使我有了更多學習的方向。最後，感謝組員的合作與幫助，才讓這次final project 能順利完成。
```

* 陳言瑄
```
這次期末專題提供了從無到有做出完整專案的機會，很有挑戰，也收穫很大。過程中，使用了一些之前沒用過的套件，學到了新的技術與除錯技巧，對前後端的架構也更加熟悉。同時透過團隊合作，有效率地討論、協作，共同完成一個專案。最後，非常感謝組員的幫助。
```


### localhost 安裝與測試之詳細步驟
#### 前端

##### 安裝依賴套件
```bash
cd frontend
yarn
```

##### 測試 & 啟動
```bash
cd frontend
yarn start
```

**前端的服務開在 `localhost:3000`**。

#### 後端

##### 安裝依賴套件
```bash
cd backend
yarn
```
##### 測試 & 啟動
```bash
cd backend
yarn start
```

##### 設定一些 environment variable
* 如果 localhost 有跑 mongodb 的話，可以不用動到 `.env` 沒關係。如果本地端沒有裝 mongodb 想要用遠端的 mongodb cluster 的話，在`backend/.env` 中設定 `MONGO_URL`。
* 在 `backend/.env` 中加入 `JWT_SECRET=<your secret>` 改成你喜歡的密碼。

**後端的服務開在 `localhost:4000`。**

### 服務內容
* Sign Up & Login
    * 使用者創建帳號密碼，並會檢查使用者名稱是否重複，以及再次輸入的密碼是否正確
    * 完成 Sign Up 後，系統會 redirect 到 Login 的頁面
    * 如果使用者尚未進行 Sign Up， 也可以透過 Login 頁面進到 Sign Up 頁面
* MainPage
    * MainPage 左側有 Dashboard，點擊可切換至不同頁面
    * 上方會顯示 Logout 按鈕，點擊可登出
    * 主畫面則會依選擇的功能顯示不同頁面
* Home / Lobby
    * 左側 table 顯示目前使用者所加入的 Chatroom 資訊，點擊 Join 可直接加入
    * 右側顯示目前在線上的朋友列表(friends online)，點擊上方 refresh 按鈕，可重新尋找在線上的朋友，而點擊訊息圖標按鈕則會在其下方顯示該朋友的資訊，資訊欄也可透過點擊 close 關閉
* Chat
    * 點選 Chat 後，會出現兩個選項： Create Room 及 Join Room
    * Create Room: 輸入欲創建聊天室的名稱與密碼（名稱若與平台現有聊天室重複，將不予通過）
    * Join  Room: 輸入欲加入聊天室的名稱。若使用者已為該聊天室成員，則可直接進入。反之，須輸入正確密碼。
    * 進入聊天室後，使用者可發送訊息，所有聊天室成員皆可於對話框看見訊息。
    * 聊天室下方有 Temporary Exit Room 及 Permanently Leave Room 的按鍵。
    * Temporary Exit Room: 會 redirect 至 Home。而使用者仍為該聊天室成員。
    * Permanently Leave Room：會 redirect 至 Home。而使用者非該聊天室成員，若欲重新加入該聊天室，須再次 Join room。
* Friends
    * 左側的 table 提供使用者搜尋其他的使用者，在搜尋框內輸入查詢字串並送出後，下方會顯示所有 "包含" 該字串的使用者名稱，以及上線狀態、follow / unfollow 的按鈕
    * 若點擊 follow ，該使用者會被加入 friends 名單，顯示在右方，且按鈕變成 unfollow
    * 點擊 friends 中的訊息圖標按鈕會在其下方顯示該朋友的資訊，資訊欄也可透過點擊 close 關閉
* Setting
    * 點選 Setting 後，可以更換頭像。並且有 Accounting Setting 與 Password Setting 的選項。
    * 點選 Select file 可於本機選擇圖片檔（.png/ .jpeg/ .gif），之後點選 Upload File， 即可設定頭像。
    * 點選 Accounting Setting 後，頁面右側將顯示使用者帳號資訊。點選 Edit 即可更改，資料更改後須按 Save， 系統才會更新帳號資訊。
    * 點選 Password Setting 後，可於頁面右側輸入新密碼與現有密碼。按下 Change 後，系統將進行驗證並更新密碼。

### 每位組員之負責項目

* 何承勳
    * 註冊與登入頁面的前端與後端
    * 部份主頁 (MainPage) 的前端
    * 增加以及創建聊天室功能的前端與後端
    * 聊天室的前端
* 施冠宇
    * 完成前後端 Friends 的所有功能，包括 search、 follow/unfollow，以及 friends 的 info、上線狀態。
    * 部分主頁 (MainPage) 的前端
* 陳言瑄
    * Setting 前端與後端
    * Lobby 後端

### 對於此課程的建議

