---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_NETWORK_CHANGE GUID について説明します。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE、WDK GUID_NDIS_STATUS_NETWORK_CHANGE ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: aff2bbbb844dd1ccd5cb39819f8a954954bcc45e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842276"
---
# <a name="guid_ndis_status_network_change"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE イベント GUID は、レイヤー3のアドレスを再ネゴシエートする必要があることを示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS またはミニポートドライバーは、ネットワークの状態の変化を報告する[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)ステータスを生成できます。

ミニポートドライバーまたは NDIS がネットワークの状態の変更を示している場合、NDIS は状態の表示を WMI クライアントの WMI GUID_NDIS_STATUS_NETWORK_CHANGE イベントに変換します。

この GUID で NDIS に用意されているデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に NDIS_NETWORK_CHANGE_TYPE 型の値が含まれています。 使用可能な値の一覧については、「 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)」を参照してください。

