---
title: GUID_NDIS_STATUS_LINK_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_LINK_STATE GUID について説明します。
ms.assetid: 7f56d211-14c7-4b8b-8d1c-ee7836b7b70a
keywords:
- GUID_NDIS_STATUS_LINK_STATE、WDK GUID_NDIS_STATUS_LINK_STATE ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee7f88b5b88bd370fcd19b21073c79a704eb582e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842280"
---
# <a name="guid_ndis_status_link_state"></a>GUID_NDIS_STATUS_LINK_STATE

GUID_NDIS_STATUS_LINK_STATE イベント GUID は、ミニポートアダプターのリンク状態が変更されたことを示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

ミニポートドライバーは、 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)状態表示を使用して、リンク状態が変更されたことを NDIS およびそれ以降のドライバーに通知します。

ミニポートドライバーによってリンク状態の変更が示されると、NDIS は状態の表示を WMI クライアントの WMI GUID_NDIS_STATUS_LINK_STATE イベントに変換します。

NDIS が GUID と共に提供するデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に[NDIS_LINK_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体が含まれています。 **NDIS_LINK_STATE**構造体は、メディアの物理的な状態を指定します。

リンクステータスの詳細については、「 [OID_GEN_LINK_STATE](oid-gen-link-state.md) and [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)」を参照してください。

