---
title: GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE GUID について説明します。
ms.assetid: f1daadff-a564-4308-82cd-525a1dae866a
keywords:
- GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE、WDK GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 619c25e57f7d6da7ad5db59bb12be753d48dcd8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842274"
---
# <a name="guid_ndis_status_offload_capabilities_change"></a>GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE

GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE イベント GUID は、NDIS ポートまたはミニポートアダプターのオフロード特性が変更されたことを示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

ミニポートドライバーは、 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状態表示を使用して、タスクオフロード機能が変更されたことを NDIS およびそれ以降のドライバーに通知します。

ミニポートドライバーによってタスクのオフロードの変更が示された場合、NDIS は状態の表示を WMI クライアントの WMI GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE イベントに変換します。

NDIS が GUID と共に提供するデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。

タスクのオフロード機能の詳細については、「 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md) and [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)」を参照してください。

