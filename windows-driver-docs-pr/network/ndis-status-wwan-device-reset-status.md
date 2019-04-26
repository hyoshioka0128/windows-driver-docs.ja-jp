---
title: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
description: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
ms.assetid: 3745E3A8-6807-4BAF-8074-90C661EAD15E
keywords:
- NDIS_STATUS_WWAN_DEVICE_RESET_STATUS、モデム リセット状態の通知、モバイル ブロード バンド モデム リセット状態の通知、MB モデム リセット状態の通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1755716139d831c4a2015db127e99eb22ddd5e0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348544"
---
# <a name="ndisstatuswwandeviceresetstatus"></a>NDIS_STATUS_WWAN_DEVICE_RESET_STATUS

NDIS_STATUS_WWAN_DEVICE_RESET_STATUS 通知は、モデム デバイスのリセットの状態の MB ホストに通知するモデムのミニポート ドライバーによって送信されます。 この通知は、非同期の応答として送信、 [OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)セットの要求。

この通知を使用して、 [NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)構造体。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>関連項目

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)

[リセット操作の MB モデム](mb-modem-reset-operations.md)

