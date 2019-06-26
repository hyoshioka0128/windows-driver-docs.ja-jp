---
title: GUID_NDIS_STATUS_LINK_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_LINK_STATE について説明します。
ms.assetid: 7f56d211-14c7-4b8b-8d1c-ee7836b7b70a
keywords:
- GUID_NDIS_STATUS_LINK_STATE、WDK GUID_NDIS_STATUS_LINK_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73b47c74a17dc0dcc6ab4a7466510c508c45b71f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382689"
---
# <a name="guidndisstatuslinkstate"></a>GUID_NDIS_STATUS_LINK_STATE

GUID_NDIS_STATUS_LINK_STATE イベント GUID では、ミニポート アダプターのリンク状態の変更があったことを示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

ミニポート ドライバーを使用して、 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)リンクの状態に変更されたが NDIS と関連付けたドライバーに通知する状態を示す値。

ミニポート ドライバーでは、リンク状態が変化することを示します、NDIS は WMI GUID_NDIS_STATUS_LINK_STATE イベントを WMI クライアントの状態表示を変換します。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)が続く構造体、 [NDIS_LINK_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。 **NDIS_LINK_STATE**構造がメディアの物理的な状態を指定します。

リンクのステータスの詳細については、次を参照してください。 [OID_GEN_LINK_STATE](oid-gen-link-state.md)と[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)します。

