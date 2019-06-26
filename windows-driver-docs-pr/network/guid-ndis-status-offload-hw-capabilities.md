---
title: GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES について説明します。
ms.assetid: 6f5e11c1-4fa0-4a9b-90f3-85a3cb8b8878
keywords:
- GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES、WDK GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296c738742425851722d1e8ad6910c2bd4e10aea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369660"
---
# <a name="guidndisstatusoffloadhwcapabilities"></a>GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES

GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES イベント GUID では、NDIS ポートまたはミニポート アダプターに関連付けられているハードウェアのオフロード特性の変更があったいることを示します。 通常、ハードウェアの変更は、追加または削除、MUX 中間ドライバーに関連付けられているハードウェアを反映します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

MUX 中間ドライバーの使用、 [NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md)オフロード機能をタスクが変更されたが NDIS と関連付けたドライバーに通知する状態を示す値。

ドライバーでは、タスクのオフロード ハードウェアの変更を示します、NDIS は WMI GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES イベントを WMI クライアントの状態表示を変換します。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)が続く構造体、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

タスクのオフロード機能の詳細については、次を参照してください。 [NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md)と[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)します。

