---
title: GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES GUID について説明します。
ms.assetid: 6f5e11c1-4fa0-4a9b-90f3-85a3cb8b8878
keywords:
- GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES、WDK GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09d9e14b384281557e8d71a6a37f749760c85336
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842330"
---
# <a name="guid_ndis_status_offload_hw_capabilities"></a>GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES

GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES イベント GUID は、NDIS ポートまたはミニポートアダプターに関連付けられているハードウェアのオフロード特性が変更されたことを示します。 ハードウェアの変更には、通常、MUX 中間ドライバーに関連付けられているハードウェアの追加または削除が反映されます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

MUX 中間ドライバーは、 [NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md)状態表示を使用して、タスクオフロード機能が変更されたことを NDIS およびそれ以降のドライバーに通知します。

ドライバーによってハードウェアのオフロードの変化が示された場合、NDIS は状態の表示を WMI クライアントの WMI GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES イベントに変換します。

NDIS が GUID と共に提供するデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。

タスクのオフロード機能の詳細については、「 [NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md) and [OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)」を参照してください。

