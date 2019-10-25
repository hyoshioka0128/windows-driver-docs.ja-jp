---
title: NDIS_STATUS_WWAN_PCO_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_PCO_STATUS 通知を使用して、以前の OID_WWAN_PCO クエリ要求の完了を MB サービスに通知します。
ms.assetid: E0F70FAE-B7C6-4BE4-B89A-88084463EEA5
keywords:
- NDIS_STATUS_WWAN_PCO_STATUS、PCO 状態通知、モバイルブロードバンド PCO 状態通知、MB PCO 状態通知
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: a289ee894c9616d4c3775a81ec9b22005a062e5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844769"
---
# <a name="ndis_status_wwan_pco_status"></a>NDIS_STATUS_WWAN_PCO_STATUS

**NDIS_STATUS_WWAN_PCO_STATUS**通知は、モデムのミニポートドライバーによって送信され、モデムの現在のプロトコル構成オプション (pco) の状態を OS に通知します。 モデムミニポートドライバーは、次の3つのシナリオでこの通知を送信します。

1.  アクティブ化された接続に新しい PCO 値が到着したとき。
2.  ホストによって接続がアクティブ化またはブリッジされたときに、モデムが PCO 値をすぐに使用できるようになったとき。
3.  ホストからの[OID_WWAN_PCO](oid-wwan-pco.md)クエリ要求への応答として。

新しい PCO 値が到着すると、この通知は要請されないため、ネットワークからの最新の PCO 値と共に送信されます。 通知は、アクティブ化された接続の PDN に対応する NDIS ポート番号で表示されます。

接続がホストからアクティブまたはブリッジされると、モデムは PCO 値がキャッシュされているかどうかを確認する必要があります。 有効になっている場合は、ホストがアクティブ化またはブリッジされた PDN に対応する NDIS ポート番号を使用して、ホストに通知を送信します。

この通知は、 **OID_WWAN_PCO**クエリ要求が完了したことをホストに通知するために使用されます。 pco 値は通知に含まれています。 ホストは、ポート番号に対応する PDN に PCO 値の完全な構造を渡すようにモデムに要求します。

PCO 機能がモデムでサポートされていても、ホストが**OID_WWAN_PCO**クエリ要求を送信したときにネットワークから pco 値が受信されなかった場合、モデムは空の WWAN_PCO_ を含む**NDIS_STATUS_WWAN_PCO_STATUS**通知を返す必要があります。 [値](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value)のペイロード。 

この通知では、 [NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)構造体が使用されます。

> [!NOTE]
> 現時点では、Windows 10 バージョン1709以降では、一部のモデムはオペレーター固有の PCO 要素しか提供できません。 PCO データ構造がモデムによって受信されても、適用可能なオペレーター固有の PCO 要素が存在しない場合、不要なデバイスのウェイクアップを避けるために、モデムは PCO 通知を OS にアドバタイズしません。 

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis. h |

## <a name="see-also"></a>関連項目

[OID_WWAN_PCO](oid-wwan-pco.md)

[NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)

[WWAN_PCO_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value)

[MB プロトコル構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
