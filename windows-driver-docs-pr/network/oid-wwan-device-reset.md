---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB デバイスのリセット、モバイルブロードバンドデバイスのリセット、モバイルブロードバンドミニポートドライバーデバイスのリセット
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685a489c1426bbd8de4bc5b52a328ad671271afb
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916800"
---
# <a name="oid_wwan_device_reset"></a>OID_WWAN_DEVICE_RESET

OID_WWAN_DEVICE_RESET は、モバイルブロードバンドホストによってモデムミニポートアダプターに送信され、モデムデバイスをリセットします。

クエリ要求は適用できません。

Set 要求の場合、OID_WWAN_DEVICE_RESET は[NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)構造体を使用します。 モデムミニポートドライバーは、要求を非同期に設定し、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻してから、モデムデバイスのリセット状態を表す[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)構造を含む[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)通知を送信する必要があります。 この応答にはペイロードは含まれていませんが、常に*WWAN_STATUS_SUCCESS*や*WWAN_STATUS_BUSY*などのモデムからのステータスコードです。

要請されていないイベントは適用できません。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1709**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)

[MB モデム リセット操作](mb-modem-reset-operations.md)

