# 方案三

審視 [方案一](../Scheme1/README.md) 以及 [方案二](../Scheme2/README.md)，從另一個角度來思考。

以最小匹配來思考，降低匹配設定複雜度，但會損失靈活的彈性設計。

> 結果不見得是最單純的，有可能會有爆炸性的 `rule_xxx`。

- 保留 `assign_rule_infos` 對應的方式來找尋的概念。

- `rule_xxx` 來設定 對應的 `env_base` 以及 `toggle_feature`

  > `env_base` 直接設定於此。
  >
  > `toggle_feature` 直接設定於此。

- 關鍵字可看[欄位說明](#欄位說明)

---
---

## 大綱

- [方案三](#方案三)
  - [大綱](#大綱)
  - [概念](#概念)
  - [欄位說明](#欄位說明)
    - [assign_rule_infos](#assign_rule_infos)
    - [rule_xxx](#rule_xxx)
  - [驗證資料合法性](#驗證資料合法性)

---
---

## 概念

- [Assign Rule Concept](../AssignRuleConcept/README.md)

  > 通用性概念。

- rule 彈性 :

  - env_base : 沒有彈性，直接設定。

  - toggle_feature : 沒有彈性，直接設定。

---
---

## 欄位說明

### assign_rule_infos

指定的規則資訊

- type : json array

  - 單一 object 格式 : jsonObject

    - name : "環境名稱"

      - type : string

      - 範例 :

      ```text
      "preDev"
      ```

    - rule_key : 對應的 rule 於 remote config 的欄位名稱

      - type : string

      - 範例 :

      ```text
      "rule_preDev"
      ```

- 範例 :

  ```json
  [
    {
      "name": "preDev",
      "rule_key": "rule_preDev"
    },
    {
      "name": "dev",
      "rule_key": "rule_dev"
    },
    {
      "name": "rc",
      "rule_key": "rule_rc"
    },
    {
      "name": "beta",
      "rule_key": "rule_beta"
    },
    {
      "name": "product",
      "rule_key": "rule_product"
    },
    {
      "name": "0.1.0",
      "rule_key": "rule_0_1_0"
    }
  ]
  ```

---

### rule_xxx

某個規則，可能是某環境，或者是指定的特殊版本。

> 命名原則， rule_[xxx]，[xxx] 盡可能與 `assign_rule_infos` 中的 [name] 一致或有關聯性。
>
> 較不易搞混。

- type: json object

  - env_base : 環境的基礎設定

    - type : json object

      - urls : 對應的網址列表

        - type : json object

          細節為 url_key : 對應的 url

          現行的 key 有 :

          - "api" : webapi 網址

          - "cdn" : 資源檔的下載網址

          - "wsLive" : websocket for 大廳

          - "wsChat" : websocket for 聊天室

          - "vipRule" : VIP規則 (內開網頁)

    - 範例 :

    ```json
    {
      "urls": {
        "api": "http://api.predev-osport.cg777.net/ClientGateway/api/",
        "cdn": "http://cdn.predev-osport.cg777.net/",
        "wsLive": "ws://www.predev-osport.cg777.net/LiveLobbySystem/primus",
        "wsChat": "ws://www.predev-osport.cg777.net/ChatRoomsSystem/primus",
        "vipRule": "http://www.predev-osport.cg777.net/#/merit"
      }
    }
    ```

  - toggle_feature : 功能開關設定

    直覺上是 on/off 的開關，不過可討論是否是一個列舉 int 概念。

    - type : json object

    - 範例 :

      ```json
      {
          "feature_a": true,
          "feature_b": false,
          "feature_c": true
      }
      ```

- 範例 :

  ```json
  {
    "env_base": {
      "urls": {
        "api": "http://api.predev-osport.cg777.net/ClientGateway/api/",
        "cdn": "http://cdn.predev-osport.cg777.net/",
        "wsLive": "ws://www.predev-osport.cg777.net/LiveLobbySystem/primus",
        "wsChat": "ws://www.predev-osport.cg777.net/ChatRoomsSystem/primus",
        "vipRule": "http://www.predev-osport.cg777.net/#/merit"
      }
    },
    "toggle_feature": {
      "feature_a": true,
      "feature_b": false,
      "feature_c": true,
      "feature_is_review": true
    }
  }
  ```

- 附註 :

  若有送審遮蔽需求，可將其設定到 toggle_feature 設定中。

  > e.g. feature_is_review : true

  這樣就不用一個獨立的 remote config 欄位。

  > e.g. review_ver : 1.0.2

---
---

## 驗證資料合法性

- check `assign_rule_infos` is legal

  - 確保 name 其對應的 `rule_key` 都有實際的內容。

  - 確保 包版中的預設 `envName` 於 `assign_rule_infos` 有找到對應的 name 。

    `envName` : 為編譯時期決定的預設環境 (default env)。

- check `rule_xxx` is legal

  由 `assign_rule_infos` 中，

  動態取得對應的 `rule_xxx`，

  並檢查每個 `rule_xxx` 都是合法的。

  - cehck `env_base` is legal

    設定的 `env_base` 是否合法。

  - check `toggle_feature` is legal

    設定的 toggle_feature 是否合法。

    > 每個 feature key 或許以 optional 設定思考比較容易達成。

---
---

[=> Top](#方案三)

[=> Go Back](../README.md)
