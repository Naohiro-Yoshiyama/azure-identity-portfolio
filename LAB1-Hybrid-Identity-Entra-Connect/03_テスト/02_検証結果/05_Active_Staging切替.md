# Entra Connect Active / Staging 切替試験仕様書兼結果報告書

## 1. 試験概要

本試験では、Microsoft Entra Connect の Active / Staging 構成において  
Active サーバー（mec01）から Staging サーバー（mec02）へ切替を実施し、  
同期処理が正常に継続されることを確認する。

本試験により、Active サーバー障害時のフェイルオーバー手順が  
正常に実行可能であることを確認する。

---

# 2. 試験対象

|項目|内容|
|---|---|
|Active サーバー|mec01|
|Staging サーバー|mec02|
|Active Directory|corp.local|
|Domain Controller|addc01 / addc02|
|試験ユーザー|testuser02|

---

# 3. Activeサーバー状態確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|SW-001|Active状態確認|① mec01 にログインする<br>② PowerShell を起動する<br>③ `Get-ADSyncScheduler` を実行する<br>④ SyncCycleEnabled を確認する<br>⑤ `True` であることを確認する<br>⑥ StagingModeEnabled を確認する<br>⑦ `False` であることを確認する<br>⑧ スクリーンショット取得する|Active状態||SW-001_active_state.png|

---

# 4. Stagingサーバー状態確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|SW-002|Staging状態確認|① mec02 にログインする<br>② PowerShell を起動する<br>③ `Get-ADSyncScheduler` を実行する<br>④ StagingModeEnabled を確認する<br>⑤ `True` であることを確認する<br>⑥ SyncCycleEnabled を確認する<br>⑦ `False` であることを確認する<br>⑧ スクリーンショット取得する|Staging状態||SW-002_staging_state.png|

---

# 5. Activeサーバー同期停止

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|SW-003|Active同期停止|① mec01 にログインする<br>② PowerShell を起動する<br>③ `Set-ADSyncScheduler -SyncCycleEnabled $false` を実行する<br>④ コマンド結果を確認する<br>⑤ `Get-ADSyncScheduler` を実行する<br>⑥ SyncCycleEnabled を確認する<br>⑦ `False` になっていることを確認する<br>⑧ スクリーンショット取得する|同期停止||SW-003_stop_sync.png|

---

# 6. StagingサーバーActive化

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|SW-004|Staging Active化|① mec02 にログインする<br>② PowerShell を起動する<br>③ `Set-ADSyncScheduler -SyncCycleEnabled $true` を実行する<br>④ `Get-ADSyncScheduler` を実行する<br>⑤ SyncCycleEnabled を確認する<br>⑥ `True` であることを確認する<br>⑦ StagingModeEnabled を確認する<br>⑧ `False` になっていることを確認する<br>⑨ スクリーンショット取得する|Active化成功||SW-004_active_switch.png|

---

# 7. Delta同期実行

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|SW-005|Delta同期確認|① mec02 にログインする<br>② PowerShell を起動する<br>③ `Start-ADSyncSyncCycle -PolicyType Delta` を実行する<br>④ コマンド結果を確認する<br>⑤ Success が表示されることを確認する<br>⑥ Synchronization Service Manager を起動する<br>⑦ Operations タブを確認する<br>⑧ Delta Sync / Export が成功していることを確認する<br>⑨ スクリーンショット取得する|同期成功||SW-005_delta_sync.png|

---

# 8. ユーザー同期確認

|試験ID|試験項目|試験手順|期待結果|結果|エビデンス|
|---|---|---|---|---|---|
|SW-006|ユーザー同期確認|① addc01 にログインする<br>② Active Directory Users and Computers を開く<br>③ SyncUsers OU を開く<br>④ testuser02 を作成する<br>⑤ mec02 で Delta Sync を実行する<br>⑥ Azure Portal を開く<br>⑦ Entra ID → Users を開く<br>⑧ testuser02 が同期されていることを確認する<br>⑨ スクリーンショット取得する|同期成功||SW-006_user_sync.png|
