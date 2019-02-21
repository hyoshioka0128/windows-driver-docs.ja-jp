---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB デバイスのリセット、モバイル ブロード バンド デバイスのリセット、ミニポート ドライバーのモバイル ブロード バンド デバイスのリセット
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009a309b889e3efbd06bf23dfa892eee7ca40e5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558385"
---
# <a name="oidwwandevicereset"></a>OID_WWAN_DEVICE_RESET

OID_WWAN_DEVICE_RESET は、モデム デバイスをリセットするモバイル ブロード バンド モデム ミニポート アダプター ホストによって送信されます。

クエリ要求には適用されません。

OID_WWAN_DEVICE_RESET を使用して、一連の要求について、 [NDIS_WWAN_SET_DEVICE_RESET](https://msdn.microsoft.com/library/windows/hardware/73894308-CFE0-49EF-BB09-E104CEE9C746)構造体。 モデムのミニポート ドライバーが要求を非同期に設定する対応する必要が最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)通知含む、 [NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)モデム デバイスのリセットの状態を表す構造体です。 この応答は、ペイロードが含まれていないが、モデムからのステータス コードがなどは常に*WWAN_STATUS_SUCCESS*または*WWAN_STATUS_BUSY*します。

要請されていないイベントは適用されません。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)

[NDIS_WWAN_SET_DEVICE_RESET](https://msdn.microsoft.com/library/windows/hardware/73894308-CFE0-49EF-BB09-E104CEE9C746)

[リセット操作の MB モデム](mb-modem-reset-operations.md)

