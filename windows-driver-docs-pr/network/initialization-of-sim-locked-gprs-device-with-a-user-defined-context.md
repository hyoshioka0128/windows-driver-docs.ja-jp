---
title: SIM ロック GPRS デバイス (ユーザー定義のコンテキスト) を初期化しています
description: ユーザー定義のコンテキストで GPRS の SIM ロックされているデバイスの初期化
ms.assetid: 655b7789-ffea-459c-9489-5c2f565b77ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c1846a5dd7b4518542a1b1e26c21313e028bf5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385089"
---
# <a name="initialization-of-sim-locked-gprs-device-with-a-user-defined-context"></a>ユーザー定義のコンテキストで GPRS の SIM ロックされているデバイスの初期化


次の図をユーザーが SIM PIN を入力し、アクセス ポイント名の文字列を手動で構成のシナリオを示しています。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![ユーザーが sim pin を入力し、アクセス ポイント名の文字列を手動で構成のシナリオを示す図](images/wwanlockedgsmdevinitseq.png)

PIN1 がロックされていると、GSM ベースのデバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_準備\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)デバイスの準備完了状態を識別するために、ミニポート ドライバーにクエリ要求。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

2.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスにサブスクライバー id モジュール (SIM) がロックされていることを示す MB サービスに障害通知します。

3.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)ミニポート ドライバーにクエリ要求。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

4.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

5.  MB サービスは、非同期 (非ブロッキング) を送信します[OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)ミニポート ドライバーに要求を設定します。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

6.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

7.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_準備ができて\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info) MB に示す MB サービスに通知をサービスします。MB デバイスの状態が**WwanReadyStateInitialized**します。

8.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_登録\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

9.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

10. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state) MB サービスに通知します。

11. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_ホーム\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

12. ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

13. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state) MB サービスに通知します。

14. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_パケット\_サービス](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)ミニポート ドライバーに要求します。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

15. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB サービスに通知します。

16. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

17. ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts) MB サービスにします。

18. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)MB サービスへの要求のセット。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

19. ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

 

 





