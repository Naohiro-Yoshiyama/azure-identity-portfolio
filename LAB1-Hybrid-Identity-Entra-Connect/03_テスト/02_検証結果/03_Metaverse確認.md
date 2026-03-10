# Entra Connect Metaverse確認 試験仕様書兼結果報告書

## 1. 試験概要

本試験では、Microsoft Entra Connect の同期エンジンにおいて  
Active Directory から取り込まれたオブジェクトが Metaverse に正常に作成されていることを確認する。

Metaverse は同期エンジンの中心となるデータベースであり、  
複数ディレクトリのオブジェクト情報を統合管理する役割を持つ。

---

# 2. 試験対象

|項目|内容|
|---|---|
|同期サーバー|mec01|
|Stagingサーバー|mec02|
|Active Directory|corp.local|
|Domain Controller|addc01 / addc02|
|試験ユーザー|testuser01|

---

# 3. Metaverse検索確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|MV-001|Metaverse検索確認|① mec01 にログインする<br>② スタートメニューを開く<br>③ Azure AD Connect を探す<br>④ Synchronization Service をクリックする<br>⑤ Synchronization Service Manager を起動する<br>⑥ Metaverse Search をクリックする<br>⑦ Object Type で `Person` または `User` を選択する<br>⑧ testuser01 を入力して検索する<br>⑨ 検索結果をスクリーンショット取得する|ユーザー表示||MV-001_metaverse_search.png|

---

# 4. Metaverseオブジェクト確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|MV-002|Metaverseオブジェクト確認|① 検索結果の testuser01 をダブルクリックする<br>② Metaverse Object Properties を開く<br>③ Attributes タブをクリックする<br>④ DisplayName を確認する<br>⑤ UserPrincipalName を確認する<br>⑥ MailNickname を確認する<br>⑦ 属性が Active Directory と一致していることを確認する<br>⑧ スクリーンショット取得する|属性一致||MV-002_attributes.png|

---

# 5. Connectorリンク確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|MV-003|Connectorリンク確認|① Metaverse Object Properties を開く<br>② Connectors タブをクリックする<br>③ Active Directory Connector を確認する<br>④ corp.local Connector が表示されることを確認する<br>⑤ Connector Type を確認する<br>⑥ AD Connector がリンクされていることを確認する<br>⑦ スクリーンショット取得する|AD Connectorリンク||MV-003_connector_link.png|

---

# 6. 属性統合確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|MV-004|属性統合確認|① Metaverse Object Properties を開く<br>② Attributes タブをクリックする<br>③ DisplayName を確認する<br>④ GivenName を確認する<br>⑤ Surname を確認する<br>⑥ UserPrincipalName を確認する<br>⑦ 属性が Active Directory 由来であることを確認する<br>⑧ スクリーンショット取得する|属性統合||MV-004_attribute.png|

---

# 7. Entra Connectorリンク確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|MV-005|Entra Connectorリンク確認|① Metaverse Object Properties を開く<br>② Connectors タブをクリックする<br>③ Azure Active Directory Connector を確認する<br>④ Connector が表示されていることを確認する<br>⑤ Connector Type を確認する<br>⑥ Entra ID Connector がリンクされていることを確認する<br>⑦ スクリーンショット取得する|Entra Connectorリンク||MV-005_aad_connector.png|
