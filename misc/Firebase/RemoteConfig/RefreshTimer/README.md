# Remote Config Refresh Timer

簡單描述一下 Remote Config 的更新時機。

- 撰寫文件時間 : 2021-06-01

---
---

## 大綱

- [Remote Config Refresh Timer](#remote-config-refresh-timer)
  - [大綱](#大綱)
  - [概念](#概念)
  - [延伸議題](#延伸議題)
    - [延伸功能](#延伸功能)
    - [替代方案](#替代方案)
  - [參考](#參考)

---
---

## 概念

- 本地紀錄上次取得更新時間

  > 若可由 Firebase Remote Config SDK 得知，可直接使用。

- 設定最少的間隔時間

  以 15~20 分為範圍 (不超過 firebase 的限制，由之前的產品經驗，印象是一個小時可以取四次)

- 若知道維護期間

  若知道是維護期間，則於維護時間時先不取更新，

  可於維護結束後，強制更新一次。

- 使用者沒有遇到維護，距離上次開啟 App 超過遇到的時間間隔，

  更新一次

**進階 :**

- 有後端配合

  - 可以由 `後端` (websocket) 發出通知有 remote config 異動。

    客端收到後盡可能快速更新。

    > 主要是已經登入後的更新。

---
---

## 延伸議題

### 延伸功能

**Remote Config 的推播通知 :**

Firebase 有一個是 [推播通知][Firebase雲消息傳遞] 的功能，

來通知有 Remote Config 更新，

App 端收到可去更新 Remote Config，

不過這個功能最主要問題就是強更資訊在上面，

而推播有不保證送達這個條件不符合我們的需求，

且在背景狀態下，使用者也不見得會按下推播中心的推播來啟動 App。

> 不確定性太高了，推播最好當作加強，而非必要功能。

---

### 替代方案

**Real Time DB :**

另一個替代方案是用 real-time data base，

> 即時的資料庫，修正後立即更新。
>
> Firebase 有對應功能，可參考 [Firebase Realtime Database] ，需要付費。

由於我們的用法應該都在維護期間來調整 Remote Config 居多，

所以還可以不用到這個。

只要確定使用情境可以大部分使用者都有考慮到即可。

---
---

## 參考

- [Firebase雲消息傳遞]

- [Firebase Realtime Database]

<!-- 連結設定 -->
[Firebase雲消息傳遞]: https://firebase.google.com/docs/cloud-messaging

[Firebase Realtime Database]: https://firebase.google.com/docs/database

---
---

[=> Top](#remote-config-refresh-timer)

[=> Go Back](../README.md)
