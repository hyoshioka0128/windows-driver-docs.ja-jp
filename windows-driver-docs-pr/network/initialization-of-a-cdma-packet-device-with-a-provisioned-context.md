---
title: プロビジョニング済みコンテキストでの CDMA パケット デバイスの初期化
description: プロビジョニング済みコンテキストでの CDMA パケット デバイスの初期化
ms.assetid: 07b4881c-b8df-4831-b0d3-521d187e4232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52c91035decbb18fe6ec23b264987685bc0d307a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385094"
---
# <a name="initialization-of-a-cdma-packet-device-with-a-provisioned-context"></a>プロビジョニング済みコンテキストでの CDMA パケット デバイスの初期化


次の図は、CDMA ベースのデバイスの最適なユーザー エクスペリエンスを示します。 既定のエクスペリエンスでは、ユーザーの構成は必要ありません。 このシナリオでは、CDMA ベースのアカウントがアクティブにしないことを前提としています。 GSM ベースのデバイスとは異なり、CDMA ベースのデバイスで自動的に開始登録ネットワーク アクティブ化が完了した後。 太字のラベルは、OID 識別子またはトランザクションのフロー制御を通常のテキストに表示されるラベル OID 構造内で重要なフラグ。

![モバイル ブロード バンド デバイスの初期化を cdma ベースのシーケンスを示す図](images/wwancdmadevinitseq.png)

プロビジョニングのコンテキストでパケットの CDMA ベース デバイスを初期化するには、次の手順を実装します。

1.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_準備\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

2.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスの失敗。

3.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_サービス\_アクティベーション](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-service-activation)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

4.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

5.  ミニポート ドライバーに送信[ **NDIS\_状態\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state) MB サービスにします。

6.  ミニポート ドライバーに送信[ **NDIS\_状態\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state) MB サービスにします。

7.  ミニポート ドライバー送信[ **NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service) MB サービスにします。

8.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_ホーム\_プロバイダー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-home-provider)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認で応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

9.  ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

10. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)ミニポート ドライバーにします。 ミニポート ドライバーが一時的な受信確認応答 (NDIS\_状態\_を示す値\_必須)、要求を受信したことと、将来の必要な情報の通知を送信するされます。

11. ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

12. MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)ミニポート ドライバーにします。 一時的な受信確認応答ミニポート ドライバー (NDIS\_状態\_を示す値\_REQUIRED)、要求を受信したことに必要な情報、今後の通知は送信。

13. ミニポート ドライバー送信 NDIS\_状態\_WWAN\_MB サービスに成功します。

14. ミニポート ドライバー送信[ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state) MB サービスにします。

 

 





