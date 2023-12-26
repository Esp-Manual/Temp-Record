# Assign Rule Concept

---
---

## 大綱

- [Assign Rule Concept](#assign-rule-concept)
  - [大綱](#大綱)
  - [說明](#說明)
  - [概念](#概念)
  - [範例](#範例)
    - [範例 A](#範例-a)
    - [範例 B](#範例-b)
  - [補充](#補充)
    - [rule 彈性](#rule-彈性)
  - [參考](#參考)

---
---

## 說明

目前所有的方案，都有個共同的概念，集中於此來說明。

不同的方案差異在於細節的頗析不同。

> Rule 頗析規則細節不同，後續說明。

---
---

## 概念

- assign_rule_infos :

  裡面的資訊會去匹配名稱對應的規則。

- rule_xxx :

  某個規則。

- 流程 :

  App 抓到 remote config 資訊時，

  `驗證資料合法性` 後，

  > 驗證資料牽涉到細節，須參考各自方案的 `驗證資料合法性` 的做法。

  都合法再檢查 客端版本是否於 `assign_rule_infos` 找到對應的 name，

  - 有匹配 : 與客端的版本一樣的名稱

    以該對應的 `rule` 為設定內容。

  - 沒有匹配 : 找不到與客端的版本一樣的名稱

    則以此編譯時的 `envName` 當作預設環境。

    找其預設環境對應的 `rule` 套用，

---
---

## 範例

某次的 [iOS] 線上送審，遇到`後端`無法作向下相容，

此時需要做送審環境的指定環境功能。

**範例的通用條件:**

- 出版時編譯環境

  envName : product

  > 此為 default envName，編譯時期決定。

- compatibility_versions

  相容清單 :

  ```js
  [1.0.0,1.0.1,1.0.2]
  ```

- 送審版本 : 1.0.2

- assign_rule_infos

  指定規則資訊

  ```json
  [
    {
      "name": "product",
      "rule_key": "rule_product"
    },
    {
      "name": "1.0.1",
      "rule_key": "rule_product_review"
    }
  ]
  ```

---

### 範例 A

此版本為架上的版本。

- info.plist

  CFShortVersion : "1.0.0"

  > iOS 的 release 版本，相容性清單的比對基準。

**說明 :**

CFShortVersion 有在 compatibility_versions 中，

且在 assign_rule_infos 並無對應的 name : "1.0.0"，

則會以 envName : product 對應的 `rule_product` 內容，

當做其對應環境的相關資訊。

---

### 範例 B

此版本為送審版本。

- info.plist

  CFShortVersion : "1.0.1"

  > iOS 的 release 版本，相容性清單的比對基準。

**說明 :**

CFShortVersion 有在 compatibility_versions 中，

且在 assign_rule_infos 有找到對應的 name : "1.0.1"，

則規則會以 `rule_product_review` 的實際內容來指定其還境相關資訊。

---
---

## 補充

不同的方案差異在於 rule 的內容定義。

**rule 項目 :**

rule 中主要涵蓋兩部分。

- env_base

  對應環境的基本設定。

- toggle_feature

  功能開關設定。

---

### rule 彈性

不同的方案主要差異為 rule 的彈性到什麼程度為何。

- 彈性 :

  env_base ， toggle_feature 的組合程度。

  彈性越大表示越能夠組合。

依照不同的方案會有可能新增其他的 remote config 欄位來輔助。

- 彈性的比較表 :

  | 方案\功能 |   env_base   | toggle_feature |
  |:---------:|:------------:|:--------------:|
  |   [方案一]  | 部分組合彈性 |    直接設定    |
  |   [方案二]  | 部分組合彈性 |   可組合彈性   |
  |   [方案三]  |   直接設定   |    直接設定    |
  |   [方案四]  |  可組合彈性  |   可組合彈性   |

  **說明 :**

  - 部分組合彈性 :

    該功能有另外的集中的設定欄位，

    rule 中對應中的此功能對應是設定該功能的 key name，

    會去集中的欄位中找尋對應內容。

    - 範例 :

      env_base 為部分組合彈性。

      統一設定於 env_base_infos。

      rule 中 env_base 的 value ， 會在 env_base_infos 找尋到對應設定資料。

  - 可組合彈性 :

    該功能也是使用 assign 的概念，

    與 assign rule 的概念相容。

  - 直接設定 :

    直接在 rule 中對應的功能設定。

---
---

## 參考

- [方案一]

- [方案二]

- [方案三]

- [方案四]

<!-- 連結設定 -->
[方案一]: ../Scheme1/README.md
[方案二]: ../Scheme2/README.md
[方案三]: ../Scheme3/README.md
[方案四]: ../Scheme4/README.md

---
---

[=> Top](#assign-rule-concept)

[=> Go Back](../README.md)
