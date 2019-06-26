---
title: GUID_NDIS_STATUS_PORT_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_PORT_STATE について説明します。
ms.assetid: c657eef6-eb80-4715-9d60-0d2dde403300
keywords:
- GUID_NDIS_STATUS_PORT_STATE、WDK GUID_NDIS_STATUS_PORT_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7413087988a808903d0557500d3e8f09ef405661
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366640"
---
# <a name="guidndisstatusportstate"></a>GUID_NDIS_STATUS_PORT_STATE

GUID_NDIS_STATUS_PORT_STATE イベント GUID では、NDIS ポートの状態の変更を示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS ポートの使用をサポートするミニポート ドライバー、 [NDIS_STATUS_PORT_STATE](ndis-status-port-state.md) NDIS ポートの状態の変化を示すステータスを示す値。

ミニポート ドライバーでは、ポートの状態が変更されたことを示します、NDIS は WMI GUID_NDIS_STATUS_PORT_STATE イベントを WMI クライアントの状態表示を変換します。

この GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)が続く構造体、 [NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_GEN_PORT_STATE](oid-gen-port-state.md)します。

