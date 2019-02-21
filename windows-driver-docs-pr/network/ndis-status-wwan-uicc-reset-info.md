---
title: NDIS_STATUS_WWAN_UICC_RESET_INFO
description: NDIS_STATUS_WWAN_UICC_RESET_INFO
ms.assetid: ADA3ADC9-82AD-423A-ABA4-902EAF5F5C74
keywords:
- NDIS_STATUS_WWAN_UICC_RESET_INFO、UICC リセット状態の通知、モバイル ブロード バンド UICC リセット状態の通知、MB UICC リセット状態の通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6deb8a53742bb47118eb823eefd43633a93e2b09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552247"
---
# <a name="ndisstatuswwanuiccresetinfo"></a>NDIS_STATUS_WWAN_UICC_RESET_INFO

NDIS_STATUS_WWAN_UICC_RESET_INFO 状態の通知は、UICC スマート カードにパススルーの現在の状態の MB ホストに通知するモデム ミニポート アダプターによって送信されます。 Folloiwng の 2 つのシナリオでは、この通知が送信されます。

1. 後に、 [OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)クエリ要求。
2. UICC リセットが完了したら UICC カードの後のリセットのパススルー状態の MB ホストに通知する、要求の設定に従って、OID_WWAN_UICC_RESET。

この通知を使用して、 [NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)構造体。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>関連項目

[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)

[NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)

[低レベルの MB UICC アクセス](mb-low-level-uicc-access.md)

