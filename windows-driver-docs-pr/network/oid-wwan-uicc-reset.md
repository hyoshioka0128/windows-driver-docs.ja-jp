---
title: OID_WWAN_UICC_RESET
description: OID_WWAN_UICC_RESET
ms.assetid: D6654B8D-8700-437B-A944-BB273C7D31A1
keywords:
- MB UICC のリセットは、モバイル ブロード バンド UICC リセット、UICC リセット モバイル ブロード バンドのミニポート ドライバー
ms.date: 08/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 044af332f0d583ecb6a51394c5934be322ae00fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385491"
---
# <a name="oidwwanuiccreset"></a>OID_WWAN_UICC_RESET

OID_WWAN_UICC_RESET モバイル ブロード バンド ホスト UICC スマート カードをリセットして、リセット後 UICC のパススルーの状態を指定またはアダプターのパススルー状態をクエリするモデム ミニポート アダプターに送信されます。

モデムのミニポート ドライバーする必要がありますクエリ要求を処理、非同期的に最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)通知含む、 [NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)を格納する構造体、 [WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_uicc_reset_info)アダプターのパススルー状態を表す構造体です。

OID_WWAN_UICC_RESET を使用して、一連の要求について、 [NDIS_WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_uicc_reset)を格納する構造体、 [WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_set_uicc_reset)パススルー アクション、ホストを表す構造体UICC をリセットした後に、ミニポート アダプターを指定します。 ミニポート アダプタはで応答のリセットが完了した後、 **NDIS_STATUS_WWAN_UICC_RESET_INFO**を格納するには、通知、 [NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)構造体を示すために、そのパススルー状態です。

要請されていないイベントは適用されません。

パススルー操作とパススルー状態に関する詳細については、次を参照してください。 [MB 低レベル UICC アクセス](mb-low-level-uicc-access.md)します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)

[WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_uicc_reset_info)

[NDIS_WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_uicc_reset)

[WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_set_uicc_reset)

[NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)

[低レベルの MB UICC アクセス](mb-low-level-uicc-access.md)

