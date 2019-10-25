---
title: GUID_NDIS_STATUS_PORT_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_PORT_STATE GUID について説明します。
ms.assetid: c657eef6-eb80-4715-9d60-0d2dde403300
keywords:
- GUID_NDIS_STATUS_PORT_STATE、WDK GUID_NDIS_STATUS_PORT_STATE ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: c314ac9e32e9285af553cdfde32ea8ab7985d3d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842370"
---
# <a name="guid_ndis_status_port_state"></a>GUID_NDIS_STATUS_PORT_STATE

GUID_NDIS_STATUS_PORT_STATE イベント GUID は、NDIS ポートの状態が変更されたことを示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS ポートをサポートするミニポートドライバーは、 [NDIS_STATUS_PORT_STATE](ndis-status-port-state.md)状態を示し、ndis ポートの状態の変化を示します。

ミニポートドライバーによってポートの状態の変更が示されると、NDIS は状態の表示を WMI クライアントの WMI GUID_NDIS_STATUS_PORT_STATE イベントに変換します。

この GUID で NDIS に用意されているデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に[NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)構造体が含まれています。

ポートの状態の詳細については、「 [OID_GEN_PORT_STATE](oid-gen-port-state.md)」を参照してください。

