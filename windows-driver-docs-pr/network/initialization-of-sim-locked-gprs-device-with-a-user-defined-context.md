---
title: SIM ロック GPRS デバイス (ユーザー定義のコンテキスト) を初期化しています
description: ユーザー定義のコンテキストで GPRS の SIM ロックされているデバイスの初期化
ms.assetid: 655b7789-ffea-459c-9489-5c2f565b77ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc79ad5fa8939f99701af906a45e6b432bb5df9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379835"
---
# <a name="initialization-of-sim-locked-gprs-device-with-a-user-defined-context"></a>ユーザー定義のコンテキストで GPRS の SIM ロックされているデバイスの初期化


次の図をユーザーが SIM PIN を入力し、アクセス ポイント名の文字列を手動で構成のシナリオを示しています。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![ユーザーが sim pin を入力し、アクセス ポイント名の文字列を手動で構成のシナリオを示す図](images/wwanlockedgsmdevinitseq.png)

PIN1 がロックされていると、GSM ベースのデバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_準備\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569833)デバイスの準備完了状態を識別するために、ミニポート ドライバーにクエリ要求。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

2.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスにサブスクライバー id モジュール (SIM) がロックされていることを示す MB サービスに障害通知します。

3.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)ミニポート ドライバーにクエリ要求。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

4.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

5.  MB サービスは、非同期 (非ブロッキング) を送信します[OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)ミニポート ドライバーに要求を設定します。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

6.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

7.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_準備ができて\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567856) MB に示す MB サービスに通知をサービスします。MB デバイスの状態が**WwanReadyStateInitialized**します。

8.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_登録\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569834)ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

9.  ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

10. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567857) MB サービスに通知します。

11. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_ホーム\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/ff569826)ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

12. ミニポート ドライバーに送信する NDIS\_状態\_WWAN\_MB サービスに成功通知します。

13. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567857) MB サービスに通知します。

14. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_パケット\_サービス](https://msdn.microsoft.com/library/windows/hardware/ff569827)ミニポート ドライバーに要求します。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

15. ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB サービスに通知します。

16. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://msdn.microsoft.com/library/windows/hardware/ff569831)ミニポート ドライバーにクエリ要求。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

17. ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff567854) MB サービスにします。

18. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://msdn.microsoft.com/library/windows/hardware/ff569831)MB サービスへの要求のセット。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

19. ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

 

 





