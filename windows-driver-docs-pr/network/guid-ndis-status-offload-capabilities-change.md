---
title: GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE について説明します。
ms.assetid: f1daadff-a564-4308-82cd-525a1dae866a
keywords:
- GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE、WDK GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f757fbd13f7ea62051f8ee7bf37b92867c479e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369666"
---
# <a name="guidndisstatusoffloadcapabilitieschange"></a>GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE

GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE イベント GUID では、NDIS ポートまたはミニポート アダプターのオフロード特性の変更があったいることを示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

ミニポート ドライバーを使用して、 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)オフロード機能をタスクが変更されたが NDIS と関連付けたドライバーに通知する状態を示す値。

ミニポート ドライバーでは、タスクのオフロード変更を示します、NDIS は WMI GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE イベントを WMI クライアントの状態表示を変換します。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)が続く構造体、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

タスクのオフロード機能の詳細については、次を参照してください。 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)と[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)します。

