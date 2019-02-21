---
title: NDIS_STATUS_WWAN_NETWORK_BLACKLIST
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_NETWORK_BLACKLIST クエリまたは一連の要求の完了を通知するために、NDIS_STATUS_WWAN_NETWORK_BLACKLIST 通知を使用します。
ms.assetid: 38ED7C51-D352-4B48-BF80-433A7C4642AB
ms.date: 08/21/2018
keywords: -NDIS_STATUS_WWAN_NETWORK_BLACKLIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c1b00724a44e8af2514d54a4d8d9c0104a51771f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560863"
---
# <a name="ndisstatuswwannetworkblacklist"></a>NDIS_STATUS_WWAN_NETWORK_BLACKLIST

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_NETWORK_BLACKLIST**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)の照会または設定要求。

要請されていないイベントが送信されるは、ブラック リストの状態のいずれかが変更された場合の作動に作動しない、またはその逆です。 たとえば、次のように、SIM には、プロバイダーのプロバイダーの SIM ブラック リストに一致が挿入される場合です。

この通知を使用して、 [ **NDIS_WWAN_NETWORK_BLACKLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB のネットワーク ブラック リストの操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)

[OID_WWAN_NETWORK_BLACKLIST](oid-wwan-network-blacklist.md)

[**NDIS_WWAN_NETWORK_BLACKLIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_blacklist)
