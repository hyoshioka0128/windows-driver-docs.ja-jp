---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB デバイスのリセット、モバイル ブロード バンド デバイスのリセット、ミニポート ドライバーのモバイル ブロード バンド デバイスのリセット
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03397a121a25efad0dcc420030bbc32e239f666b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362846"
---
# <a name="oidwwandevicereset"></a>OID_WWAN_DEVICE_RESET

OID_WWAN_DEVICE_RESET は、モデム デバイスをリセットするモバイル ブロード バンド モデム ミニポート アダプター ホストによって送信されます。

クエリ要求には適用されません。

OID_WWAN_DEVICE_RESET を使用して、一連の要求について、 [NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)構造体。 モデムのミニポート ドライバーが要求を非同期に設定する対応する必要が最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)通知含む、 [NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)モデム デバイスのリセットの状態を表す構造体です。 この応答は、ペイロードが含まれていないが、モデムからのステータス コードがなどは常に*WWAN_STATUS_SUCCESS*または*WWAN_STATUS_BUSY*します。

要請されていないイベントは適用されません。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)

[リセット操作の MB モデム](mb-modem-reset-operations.md)

