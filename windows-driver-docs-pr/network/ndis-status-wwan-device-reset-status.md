---
title: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
description: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
ms.assetid: 3745E3A8-6807-4BAF-8074-90C661EAD15E
keywords:
- NDIS_STATUS_WWAN_DEVICE_RESET_STATUS、モデムリセット状態通知、モバイルブロードバンドモデムリセット状態通知、MB モデムリセット状態通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd39c586735ba50542471ba896b0eba62f2c7788
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842630"
---
# <a name="ndis_status_wwan_device_reset_status"></a>NDIS_STATUS_WWAN_DEVICE_RESET_STATUS

NDIS_STATUS_WWAN_DEVICE_RESET_STATUS 通知は、モデムミニポートドライバーによって送信され、モデムデバイスのリセット状態を MB ホストに通知します。 この通知は、 [OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md) set 要求への非同期応答として送信されます。

この通知では、 [NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)構造体が使用されます。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis. h |

## <a name="see-also"></a>関連項目

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[MB のモデムリセット操作](mb-modem-reset-operations.md)

