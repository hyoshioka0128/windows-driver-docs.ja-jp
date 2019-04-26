---
title: プロビジョニング済みコンテキストでの CDMA パケット デバイスの初期化
description: プロビジョニング済みコンテキストでの CDMA パケット デバイスの初期化
ms.assetid: 07b4881c-b8df-4831-b0d3-521d187e4232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec11d588984d99b13bda1d58525d8862e6274da2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339111"
---
# <a name="initialization-of-a-cdma-packet-device-with-a-provisioned-context"></a>プロビジョニング済みコンテキストでの CDMA パケット デバイスの初期化


次の図は、CDMA ベースのデバイスの最適なユーザー エクスペリエンスを示します。 既定のエクスペリエンスでは、ユーザーの構成は必要ありません。 このシナリオでは、CDMA ベースのアカウントがアクティブにしないことを前提としています。 GSM ベースのデバイスとは異なり、CDMA ベースのデバイスで自動的に開始登録ネットワーク アクティブ化が完了した後。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![モバイル ブロード バンド デバイスの初期化を cdma ベースのシーケンスを示す図](images/wwancdmadevinitseq.png)

プロビジョニングのコンテキストでパケットの CDMA ベース デバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_準備\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569833)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

2.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスの失敗。

3.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_サービス\_アクティベーション](https://msdn.microsoft.com/library/windows/hardware/ff569835)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

4.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

5.  ミニポート ドライバーに送信[ **NDIS\_状態\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567857) MB サービスにします。

6.  ミニポート ドライバーに送信[ **NDIS\_状態\_WWAN\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567857) MB サービスにします。

7.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567850) MB サービスにします。

8.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_ホーム\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/ff569826)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

9.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

10. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://msdn.microsoft.com/library/windows/hardware/ff569831)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

11. ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

12. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://msdn.microsoft.com/library/windows/hardware/ff569831)ミニポート ドライバーにします。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

13. ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

14. ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391) MB サービスにします。

 

 





