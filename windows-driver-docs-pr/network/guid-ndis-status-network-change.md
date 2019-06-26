---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_NETWORK_CHANGE について説明します。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE、WDK GUID_NDIS_STATUS_NETWORK_CHANGE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55cadd37180a81e71cbbac256450f30bbf998d39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382681"
---
# <a name="guidndisstatusnetworkchange"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE イベント GUID では、レイヤー 3 のアドレスが再度ネゴシエートされることを示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS またはミニポート ドライバーが生成することができます、 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)ネットワークの状態の変更を報告する状態を示す値。

ミニポート ドライバーまたは NDIS は、ネットワークの状態の変化を示す、NDIS は WMI GUID_NDIS_STATUS_NETWORK_CHANGE イベントを WMI クライアントの状態表示を変換します。

この GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header) NDIS_NETWORK_CHANGE_TYPE 型の値が続く構造体。 使用可能な値については、次を参照してください。 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)します。

