---
title: NDIS_STATUS_WWAN_PCO_STATUS
description: ミニポート ドライバーでは、MB サービスに前回 OID_WWAN_PCO クエリ要求の完了を通知するために、NDIS_STATUS_WWAN_PCO_STATUS 通知を使用します。
ms.assetid: E0F70FAE-B7C6-4BE4-B89A-88084463EEA5
keywords:
- NDIS_STATUS_WWAN_PCO_STATUS、PCO 状態の通知、モバイル ブロード バンド PCO 状態の通知、MB PCO 状態の通知
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dd9700bb4d0f03ea842e161b6e18b720af77989
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374810"
---
# <a name="ndisstatuswwanpcostatus"></a>NDIS_STATUS_WWAN_PCO_STATUS

**NDIS_STATUS_WWAN_PCO_STATUS**モデムの現在のプロトコルの構成オプション (PCO) 状態の OS を通知するために、モデムのミニポート ドライバーによって通知が送信されます。 モデムのミニポート ドライバーでは、次の 3 つのシナリオでこの通知を送信します。

1.  ときに新しい PCO 値は、アクティブ化された接続に到着しました。
2.  ときに、モデムでは、接続がアクティブ化またはホストがブリッジされるときにすぐに使用できる PCO 値があります。
3.  応答、 [OID_WWAN_PCO](oid-wwan-pco.md)ホストからのクエリ要求。

新しい PCO 値が到着すると、要請していないと、ネットワークからの最新の PCO 値と共に送信される、この通知になります。 通知が付属対応する NDIS ポート番号、アクティブな接続の PDN にします。

接続がアクティブ化またはホストからブリッジ、モデムがない、またはキャッシュ PCO 値があるかどうかを確認する必要があります。 場合は、ホストがアクティブ化またはブリッジ PDN に対応する NDIS ポート番号を持つホストに通知を送信します。

この通知を使用してホストに通知する、 **OID_WWAN_PCO**クエリ要求が完了したら、通知に含める PCO 値を使用します。 ホストのポート番号に対応する PDN PCO 値の完全な構造を渡すにはモデムが必要です。

モデム PCO 機能がサポートされていますが、ホストに送信するときに、ネットワークから PCO 値を受信していないかどうか、 **OID_WWAN_PCO**クエリ要求では、モデムが返すようにする、 **NDIS_STATUS_WWAN_PCO_STATUS**空の通知[WWAN_PCO_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_pco_value)ペイロード。 

この通知を使用して、 [NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)構造体。

> [!NOTE]
> 現時点では、Windows 10 バージョン 1709 以降で一部のモデム、のみ PCO 要素の特定の演算子を提供できます。 モデムが PCO データ構造体を受信した演算子の適用可能な特定 PCO 要素が存在しない場合、不要なデバイスのウェイク アップを回避するために、モデムする必要がありますアドバタイズしない os PCO 通知。 

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>関連項目

[OID_WWAN_PCO](oid-wwan-pco.md)

[NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)

[WWAN_PCO_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_pco_value)

[MB プロトコルの構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
