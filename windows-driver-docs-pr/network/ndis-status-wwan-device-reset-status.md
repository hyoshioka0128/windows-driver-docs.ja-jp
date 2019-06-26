---
title: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
description: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
ms.assetid: 3745E3A8-6807-4BAF-8074-90C661EAD15E
keywords:
- NDIS_STATUS_WWAN_DEVICE_RESET_STATUS、モデム リセット状態の通知、モバイル ブロード バンド モデム リセット状態の通知、MB モデム リセット状態の通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2521d0b1d6d2df97bc8591a24419937bb53c8231
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366620"
---
# <a name="ndisstatuswwandeviceresetstatus"></a>NDIS_STATUS_WWAN_DEVICE_RESET_STATUS

NDIS_STATUS_WWAN_DEVICE_RESET_STATUS 通知は、モデム デバイスのリセットの状態の MB ホストに通知するモデムのミニポート ドライバーによって送信されます。 この通知は、非同期の応答として送信、 [OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)セットの要求。

この通知を使用して、 [NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)構造体。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>関連項目

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[リセット操作の MB モデム](mb-modem-reset-operations.md)

