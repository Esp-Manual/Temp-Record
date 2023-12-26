# 1st_2021-04-16

目前已經有的內容說明，於 2021-04-16 的版本。

先定義為第一版的 reomote config 功能。

---
---

## 大綱

- [1st_2021-04-16](#1st_2021-04-16)
  - [大綱](#大綱)
  - [欄位說明](#欄位說明)
    - [flavorName](#flavorname)
    - [app_updeta_url](#app_updeta_url)
    - [compatibility_versions](#compatibility_versions)
    - [evnValue](#evnvalue)
    - [latest_version](#latest_version)

---
---

## 欄位說明

---

### flavorName
  
對應 firebase project 的名稱

- type : string

- 範例 :

  - 官方環境對應的 firebase project

    ```text
    official
    ```

  - 實驗環境對應的 firebase project

    ```text
    experiment
    ```

---

### app_updeta_url

對應的商店連結:

- type : string

- 範例 : (目前是測試用的，有正式商店 url 需調整)

  - 平台

    - Android:

      ```text
      http://eggworkshop.myds.me/test3/BoTV_android.html
      ```

    - iOS:

      ```text
      https://eggworkshop.myds.me/test3/BoTV_iOS.html
      ```

---

### compatibility_versions

版本相容性清單:陣列字串

- type : json array

- 範例 :

  - Android : 對應於 VersionCode

    ```json
    ["6","7","8"]
    ```

  - iOS : 對應於 BundleShortVersion

    ```json
    ["0.1.0","0.1.1"]
    ```

---

### evnValue

對應環境的名稱及相關 url

- type : json array

- 範例 :

  ```json
  [
    {
      "env": "preDev",
      "url": {
        "api": "http://api.predev-osport.cg777.net/ClientGateway/api/",
        "cdn": "http://cdn.predev-osport.cg777.net/",
        "wsLive": "ws://www.predev-osport.cg777.net/LiveLobbySystem/primus",
        "wsChat": "ws://www.predev-osport.cg777.net/ChatRoomsSystem/primus"
      }
    },
    {
      "env": "dev",
      "url": {
        "api": "http://api.dev-botv.cg777.net/ClientGateway/api/",
        "cdn": "http://cdn.dev-botv.cg777.net/",
        "wsLive": "ws://www.dev-botv.cg777.net/LiveLobbySystem/primus",
        "wsChat": "ws://www.dev-botv.cg777.net/ChatRoomsSystem/primus"
      }
    },
    {
      "env": "rc",
      "url": {
        "api": "http://api.rc-botv.cg777.net/ClientGateway/api/",
        "cdn": "http://cdn.rc-botv.cg777.net/",
        "wsLive": "ws://www.rc-botv.cg777.net/LiveLobbySystem/primus",
        "wsChat": "ws://www.rc-botv.cg777.net/ChatRoomsSystem/primus"
      }
    },
    {
      "env": "beta",
      "url": {
        "api": "https://api.botvlive.net/ClientGateway/api/",
        "cdn": "https://cdn.botvlive.net/",
        "wsLive": "wss://www.botvlive.net/LiveLobbySystem/primus",
        "wsChat": "wss://www.botvlive.net/ChatRoomsSystem/primus"
      }
    },
    {
      "env": "product",
      "url": {
        "api": "https://api.botvlive.com/ClientGateway/api/",
        "cdn": "https://cdn.botvlive.com/",
        "wsLive": "wss://game.botvlive.com/LiveLobbySystem/primus",
        "wsChat": "wss://game.botvlive.com/ChatRoomsSystem/primus"
      }
    }
  ]
  ```

---

### latest_version

商店上的最新版本，需注意 `official` 的設定，

需確保已經在架上可搜尋到，才能更新為最新的版本喔。

- type : string

- 範例 : (目前是測試用的，有正式商店 url 需調整)

  - 平台

    - Android:

      ```text
      "8"
      ```

    - iOS:

      ```text
      "0.1.0"
      ```

---
---

[=> Top](#1st_2021-04-16)

[=> Go Back](../README.md)
