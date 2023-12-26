# 方案四

以 [方案二](../Scheme2/README.md) env_base_infos 也使用 assgin 的概念。

> 亦即 `assign_env_base_infos`，`assign_toggle_feature_infos`，`assign_rule_infos` 可以使用同樣的指定細項邏輯，
>
> 或許思考`策略模式`來寫 assing detail 的工具。

**與 [方案二] 主要差異 :**

- 移除 `env_base_infos`

- 新增 `assign_env_base_infos`

- 新增 `env_base_info_xxx`

- 保留 `assign_toggle_feature_infos`

- 保留 `toggle_feature_xxx`

- `rule_xxx` 來設定 對應的 `env_base` 以及 `toggle_feature`

  > `env_base` from `assign_env_base_infos`
  >
  > `toggle_feature` from `assign_toggle_feature_infos`

- 關鍵字可看[欄位說明](#欄位說明)

---
---

## 大綱

- [方案四](#方案四)
  - [大綱](#大綱)
  - [概念](#概念)
  - [欄位說明](#欄位說明)
    - [assign_env_base_infos](#assign_env_base_infos)
    - [env_base_info_xxx](#env_base_info_xxx)
    - [assign_toggle_feature_infos](#assign_toggle_feature_infos)
    - [toggle_feature_xxx](#toggle_feature_xxx)
    - [assign_rule_infos](#assign_rule_infos)
  - [驗證資料合法性](#驗證資料合法性)

---
---

## 概念

- [Assign Rule Concept](../AssignRuleConcept/README.md)

  > 通用性概念。

- `assign_env_base_infos` :

  裡面的資訊會去匹配名稱對應的 env_base_info 的細部設定。

- `env_base_info_xxx` :

  某個環境的基礎設定。

  目前主要為環境對應的後端網址的資訊。

  > 非開關性質。

- `assign_toggle_feature_infos` :

  裡面的資訊會去匹配名稱對應的 toggle_feature 的細部設定。

- `toggle_feature_xxx` :

  某個 toggle_feature。

- rule 彈性 :

  - env_base : 可組合。

   > env_base 套用 assign 概念去匹配細節。

  - toggle_feature : 可組合。

    > toggle_feature 套用 assign 概念去匹配細節。

---
---

## 欄位說明

### assign_env_base_infos

指定的 env base info 資訊。

- type : json array

  - 單一 object 格式 : jsonObject

    - name : "env base info 名稱"

      原則上是對應認知的環境名稱，

      - type : string

      - 範例 :

      ```text
      "preDev"
      ```

    - env_base_info_key : 對應的 env_base_info 於 remote config 的欄位名稱

      - type : string

      - 範例 :

      ```text
      "env_base_info_preDev"
      ```

- 範例 :

  ```json
  [
    {
      "name": "preDev",
      "env_base_info_key": "env_base_info_preDev"
    },
    {
      "name": "dev",
      "env_base_info_key": "env_base_info_dev"
    },
    {
      "name": "rc",
      "env_base_info_key": "env_base_info_rc"
    },
    {
      "name": "beta",
      "env_base_info_key": "env_base_info_beta"
    },
    {
      "name": "product",
      "env_base_info_key": "env_base_info_product"
    }
  ]
  ```

---

### env_base_info_xxx

某個 env_base_info 設定。

此環境通用性的設定，非開關性質，目前主要為該環境對應的後端服務網址。

> 命名原則， env_base_info_[xxx]，[xxx] 盡可能與 `assign_env_base_infos` 中的 [name] 一致或有關聯性。
>
> 較不易搞混。

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

---

### assign_toggle_feature_infos

指定的 toggle feature 資訊。

- type : json array

  - 單一 object 格式 : jsonObject

    - name : "toggle feature 名稱"

      > 命名原則待討論，下面是隨便以代號來想
      >
      > 或許也可以用某個上線版本。
      >
      > e.g. `210528`

      - type : string

      - 範例 :

      ```text
      "banana"
      ```

    - toggle_feature_key : 對應的 toggle_feature 於 remote config 的欄位名稱

      - type : string

      - 範例 :

      ```text
      "toggle_feature_banana"
      ```

- 範例 :

  ```json
  [
    {
      "name": "210528",
      "toggle_feature_key": "toggle_feature_210528"
    },
    {
      "name": "banana",
      "toggle_feature_key": "toggle_feature_banana"
    },
    {
      "name": "alice",
      "toggle_feature_key": "toggle_feature_alice"
    }
  ]
  ```

---

### toggle_feature_xxx

某個 toggle_feature 設定。

直覺上是 on/off 的開關，不過可討論是否是一個列舉 int 概念。

> 命名原則， toggle_feature_[xxx]，[xxx] 盡可能與 `assign_toggle_feature_infos` 中的 [name] 一致或有關聯性。
>
> 較不易搞混。

- type : json object

- 範例 :

  ```json
  {
    "feature_a": true,
    "feature_b": false,
    "feature_c": true,
    "feature_is_review": true
  }
  ```

- 附註 :

  若有送審遮蔽需求，可將其設定到 toggle_feature 設定中。

  > e.g. feature_is_review : true

  這樣就不用一個獨立的 remote config 欄位。

  > e.g. review_ver : 1.0.2

---

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

---

### rule_xxx

某個規則，可能是某環境，或者是指定的特殊版本。

> 命名原則， rule_[xxx]，[xxx] 盡可能與 `assign_rule_infos` 中的 [name] 一致或有關聯性。
>
> 較不易搞混。

- type: json object

  - env_base : `env_base_ifnos` 中對應的名稱

    - type : string

    - 範例 :

    ```text
    "preDev"
    ```

- 範例 :

  ```json
  {
    "env_base": "preDev",
    "toggle_feature":"alice"
  }
  ```

---
---

## 驗證資料合法性

- check `assign_env_base_infos` is legal

  - 確保 name 其對應的 `env_base_info_key` 都有實際的內容。

- check `env_base_info_xxx` is legal

  由 `assign_env_base_infos` 中，

  動態取得對應的 `env_base_info_xxx`，

  並檢查每個 `env_base_info_xxx` 都是合法的。

  > 網址列部分每個 key 皆須設定為 required。

- check `assign_toggle_feature_infos` is legal

  - 確保 name 其對應的 `toggle_feature_key` 都有實際的內容。

- check `toggle_feature_xxx` is legal

  由 `assign_env_base_infos` 中，

  動態取得對應的 `toggle_feature_xxx`，

  並檢查每個 `toggle_feature_xxx` 都是合法的。

  > 依照 toggle feature 後來討論的規則為驗證的準則。

- check `assign_rule_infos` is legal

  - 確保 name 其對應的 `rule_key` 都有實際的內容。

  - 確保 包版中的預設 `envName` 於 `assign_rule_infos` 有找到對應的 name 。

    `envName` : 為編譯時期決定的預設環境 (default env)。

- check `rule_xxx` is legal

  由 `assign_rule_infos` 中，

  動態取得對應的 `rule_xxx`，

  並檢查每個 `rule_xxx` 都是合法的。

  - cehck `env` is legal

    指定的 `env_base` 於 `assign_env_base_infos` 有實際找到對應 `env_base_info_xxx` 內容。

  - check `toggle_feature` is legal

    指定的 `toggle_feature` 於 `assign_toggle_feature_infos` 有實際找到對應 `toggle_feature_xxx` 內容。

---
---

[=> Top](#方案四)

[=> Go Back](../README.md)
