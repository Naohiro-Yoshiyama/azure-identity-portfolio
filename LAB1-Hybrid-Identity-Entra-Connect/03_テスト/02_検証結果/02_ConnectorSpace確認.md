# Entra Connect Connector Space確認 試験仕様書兼結果報告書

## 1. 試験概要

本試験では、Microsoft Entra Connect において  
Active Directory のオブジェクトが Connector Space に正常に取り込まれていることを確認する。

Connector Space は、同期処理における各ディレクトリの接続領域であり、  
Active Directory と Microsoft Entra ID の同期データを一時的に保持する領域である。

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

# 3. AD Connector確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|CS-001|AD Connector存在確認|① mec01 にログインする<br>② スタートメニューを開く<br>③ Azure AD Connect を探す<br>④ Synchronization Service をクリックする<br>⑤ Synchronization Service Manager を起動する<br>⑥ Connectors タブをクリックする<br>⑦ Active Directory Connector を確認する<br>⑧ `corp.local` Connector が存在することを確認する<br>⑨ 画面をスクリーンショット取得する|AD Connector存在||CS-001_connector.png|

---

# 4. Connector Space検索

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|CS-002|Connector Space検索|① Synchronization Service Manager を起動する<br>② Connectors タブを開く<br>③ `corp.local` Connector を選択する<br>④ Search Connector Space をクリックする<br>⑤ 検索条件を設定する<br>⑥ testuser01 を入力する<br>⑦ Search をクリックする<br>⑧ 検索結果にユーザーが表示されることを確認する<br>⑨ スクリーンショット取得する|ユーザー表示||CS-002_search.png|

---

# 5. Connector Spaceオブジェクト確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|CS-003|Connector Spaceオブジェクト確認|① Search結果から testuser01 をダブルクリックする<br>② Connector Space Object Properties を開く<br>③ Attributes タブをクリックする<br>④ DisplayName を確認する<br>⑤ UserPrincipalName を確認する<br>⑥ MailNickname を確認する<br>⑦ AD属性と一致することを確認する<br>⑧ スクリーンショット取得する|属性一致||CS-003_attribute.png|

---

# 6. Connector Space同期状態確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|CS-004|同期状態確認|① Synchronization Service Manager を開く<br>② Connectors タブをクリックする<br>③ `corp.local` Connector を右クリックする<br>④ Search Connector Space をクリックする<br>⑤ testuser01 を検索する<br>⑥ オブジェクトを開く<br>⑦ Synchronization タブをクリックする<br>⑧ Metaverse Object がリンクされていることを確認する<br>⑨ スクリーンショット取得する|Metaverseリンク||CS-004_sync.png|

---

# 7. Pending Export確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|CS-005|Pending Export確認|① Synchronization Service Manager を起動する<br>② Connectors タブをクリックする<br>③ Azure Active Directory Connector を選択する<br>④ Search Connector Space をクリックする<br>⑤ testuser01 を検索する<br>⑥ オブジェクトを開く<br>⑦ Pending Export が存在しないことを確認する<br>⑧ Export が成功していることを確認する<br>⑨ スクリーンショット取得する|Export成功||CS-005_export.png|
