# Entra Connect Delta同期確認 試験仕様書兼結果報告書

## 1. 試験概要

本試験では、Microsoft Entra Connect において Delta同期が正常に実行され、
Active Directory の変更内容が Microsoft Entra ID に反映されることを確認する。

Delta同期は、変更されたオブジェクトのみを同期する処理であり、
通常の運用ではこの同期方式が定期的に実行される。

---

# 2. 試験対象

|項目|内容|
|---|---|
|同期サーバー|mec01|
|Stagingサーバー|mec02|
|Active Directory|corp.local|
|Domain Controller|addc01 / addc02|
|試験対象ユーザー|testuser01|

---

# 3. AD属性変更試験

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-001|ADユーザー属性変更|① addc01にログインする<br>② Active Directory Users and Computers を起動する<br>③ SyncUsers OUを開く<br>④ testuser01を右クリック → Propertices をクリックする<br>⑤ Display Name を変更する<br>⑥ OK をクリックする|属性変更成功|||

---

# 4. Delta同期実行

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-002|Delta同期実行確認|① mec01 にログインする<br>② PowerShell を起動する<br>③ Start-ADSyncSyncCycle -PolicyType Delta を実行する<br>④ Success が表示されることを確認する<br>⑤ Synchronization Service Manager の Operations タブで Delta Import / Delta Sync / Export が成功していることを確認する<br>⑥ スクリーンショット取得する|同期成功||DELTA-002_delta_sync.JPG|

---

# 5. Connector Space変更確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-003|Connector Space更新確認|① Synchronization Service Manager を起動する<br>② Connectors タブ → Active Directory Connector → Search Connector Space をクリックする<br>③ testuser01 を検索してオブジェクトを開く<br>④ 属性変更内容が反映されていることを確認する<br>⑤ スクリーンショット取得する|属性更新確認||DELTA-003_connector.JPG|

---

# 6. Metaverse更新確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-004|Metaverse更新確認|① Synchronization Service Manager → Metaverse Search をクリックする<br>② User を選択し testuser01 を検索する<br>③ オブジェクトを開き DisplayName が変更されていることを確認する<br>④ スクリーンショット取得する|Metaverse更新||DELTA-004_metaverse.JPG|

---

# 7. Entra ID更新確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-005|Entra ID属性更新確認|① Azure Portal → Microsoft Entra ID → Users → All Users を開く<br>② testuser01 を検索してユーザー詳細を開く<br>③ Display Name が AD で変更した値と一致することを確認する<br>④ スクリーンショット取得する|属性更新反映||DELTA-005_entra_update.JPG|

