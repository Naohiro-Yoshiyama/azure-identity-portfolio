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
|DELTA-001|ADユーザー属性変更|① addc01 にログインする<br>② Server Manager を開く<br>③ Tools をクリックする<br>④ Active Directory Users and Computers を起動する<br>⑤ `SyncUsers` OU を開く<br>⑥ testuser01 を右クリックする<br>⑦ Properties をクリックする<br>⑧ Display Name を変更する<br>⑨ OK をクリックする<br>⑩ 変更後画面をスクリーンショット取得する|属性変更成功||DELTA-001_ad_modify.png|

---

# 4. Delta同期実行

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-002|Delta同期実行確認|① mec01 にログインする<br>② PowerShell を起動する<br>③ 以下のコマンドを実行する<br>`Start-ADSyncSyncCycle -PolicyType Delta`<br>④ コマンド実行結果を確認する<br>⑤ `Success` が表示されることを確認する<br>⑥ Synchronization Service Manager を起動する<br>⑦ Operations タブを確認する<br>⑧ Delta Import / Delta Sync / Export が実行されていることを確認する<br>⑨ スクリーンショット取得する|同期成功||DELTA-002_delta_sync.png|

---

# 5. Connector Space変更確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-003|Connector Space更新確認|① mec01 にログインする<br>② Synchronization Service Manager を起動する<br>③ Connectors タブを開く<br>④ Active Directory Connector を選択する<br>⑤ Search Connector Space をクリックする<br>⑥ testuser01 を検索する<br>⑦ オブジェクトを開く<br>⑧ 属性変更内容が反映されていることを確認する<br>⑨ スクリーンショット取得する|属性更新確認||DELTA-003_connector.png|

---

# 6. Metaverse更新確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-004|Metaverse更新確認|① Synchronization Service Manager を起動する<br>② Metaverse Search をクリックする<br>③ User を選択する<br>④ testuser01 を検索する<br>⑤ オブジェクトを開く<br>⑥ 属性一覧を確認する<br>⑦ DisplayName が変更されていることを確認する<br>⑧ スクリーンショット取得する|Metaverse更新||DELTA-004_metaverse.png|

---

# 7. Entra ID更新確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|DELTA-005|Entra ID属性更新確認|① Azure Portal にアクセスする<br>② Microsoft Entra ID を開く<br>③ Users をクリックする<br>④ All Users を開く<br>⑤ testuser01 を検索する<br>⑥ ユーザー詳細を開く<br>⑦ Display Name を確認する<br>⑧ ADで変更した値と一致することを確認する<br>⑨ スクリーンショット取得する|属性更新反映||DELTA-005_entra_update.png|
