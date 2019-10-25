---
title: NDIS_STATUS_WWAN_UICC_RESET_INFO
description: NDIS_STATUS_WWAN_UICC_RESET_INFO
ms.assetid: ADA3ADC9-82AD-423A-ABA4-902EAF5F5C74
keywords:
- NDIS_STATUS_WWAN_UICC_RESET_INFO, UICC リセット状態通知, モバイルブロードバンド UICC リセット状態通知, MB UICC リセット状態通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838993d4501f63ab80407697d021fa54c0159ca3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834664"
---
# <a name="ndis_status_wwan_uicc_reset_info"></a>NDIS_STATUS_WWAN_UICC_RESET_INFO

NDIS_STATUS_WWAN_UICC_RESET_INFO 状態通知は、モデムミニポートアダプターによって送信され、現在のパススルーステータスの MB ホストが UICC スマートカードに通知されます。 この通知は、folloiwng 2 つのシナリオで送信されます。

1. [OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)クエリ要求の後。
2. OID_WWAN_UICC_RESET set 要求の後で UICC リセットが完了した後、UICC カードの事後リセットのパススルーステータスを MB ホストに通知します。

この通知では、 [NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)構造体が使用されます。

## <a name="requirements"></a>前提条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン1709 |
| ヘッダー | Ndis. h |

## <a name="see-also"></a>関連項目

[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)

[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)

[MB 低レベル UICC アクセス](mb-low-level-uicc-access.md)

