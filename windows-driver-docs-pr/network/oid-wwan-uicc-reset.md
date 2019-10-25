---
title: OID_WWAN_UICC_RESET
description: OID_WWAN_UICC_RESET
ms.assetid: D6654B8D-8700-437B-A944-BB273C7D31A1
keywords:
- MB UICC リセット、モバイルブロードバンド UICC リセット、モバイルブロードバンドミニポートドライバー UICC リセット
ms.date: 08/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c9613a7d44f9a07dad516102aed9f1bd78b0ed0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843768"
---
# <a name="oid_wwan_uicc_reset"></a>OID_WWAN_UICC_RESET

OID_WWAN_UICC_RESET は、モバイルブロードバンドホストからモデムミニポートアダプターに送信され、UICC スマートカードをリセットし、リセット後に UICC のパススルーステータスを指定するか、アダプターのパススルー状態を照会します。

モデムミニポートドライバーは、クエリ要求を非同期的に処理し、その後、NDIS_WWAN を含む[NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)通知を送信する前に、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻します。 [_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)構造体には、アダプターのパススルーステータスを表す[WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_reset_info)構造体が含まれています。

Set 要求の場合、OID_WWAN_UICC_RESET は[NDIS_WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_uicc_reset)構造体を使用します。この構造体には、リセット後に、ホストがミニポートアダプターに対して指定するパススルーアクションを表す[WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_set_uicc_reset)構造体が含まれています。UICC。 リセットが完了すると、ミニポートアダプターは**NDIS_STATUS_WWAN_UICC_RESET_INFO**通知で応答します。この通知には、パススルーステータスを示す[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)構造体が含まれています。

要請されていないイベントは適用できません。

パススルーアクションとパススルーステータスの詳細については、「 [MB 低レベルの UICC アクセス](mb-low-level-uicc-access.md)」を参照してください。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)

[WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_reset_info)

[NDIS_WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_uicc_reset)

[WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_set_uicc_reset)

[NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)

[MB 低レベル UICC アクセス](mb-low-level-uicc-access.md)

