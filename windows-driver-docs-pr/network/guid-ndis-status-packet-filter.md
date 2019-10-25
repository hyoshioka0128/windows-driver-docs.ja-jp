---
title: GUID_NDIS_STATUS_PACKET_FILTER
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_PACKET_FILTER GUID について説明します。
ms.assetid: d842862b-5b9f-46bf-aaa9-4542b3a3e047
keywords:
- GUID_NDIS_STATUS_PACKET_FILTER、WDK GUID_NDIS_STATUS_PACKET_FILTER ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa6abc1d219850e0d1ac8d6d9712a1abcac39879
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842386"
---
# <a name="guid_ndis_status_packet_filter"></a>GUID_NDIS_STATUS_PACKET_FILTER

GUID_NDIS_STATUS_PACKET_FILTER イベント GUID は、ミニポートアダプターのパケットフィルターが変更されたことを示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS は、パケットフィルターの構成が変更されている可能性があることを示す NDIS_STATUS_PACKET_FILTER ステータスを生成します。

NDIS は、状態の表示を WMI クライアントの WMI GUID_NDIS_STATUS_PACKET_FILTER イベントに変換します。

NDIS が GUID と共に提供するデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に ULONG 値が続きます。 パケットフィルターの状態と有効な値の詳細については、「 [OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md)」を参照してください。

