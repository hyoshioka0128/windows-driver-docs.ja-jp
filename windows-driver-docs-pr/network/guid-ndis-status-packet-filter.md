---
title: GUID_NDIS_STATUS_PACKET_FILTER
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_PACKET_FILTER について説明します。
ms.assetid: d842862b-5b9f-46bf-aaa9-4542b3a3e047
keywords:
- GUID_NDIS_STATUS_PACKET_FILTER、WDK GUID_NDIS_STATUS_PACKET_FILTER ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54984c805ac7a4fd6e6825df6406d75d967b3cfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578264"
---
# <a name="guidndisstatuspacketfilter"></a>GUID_NDIS_STATUS_PACKET_FILTER

GUID_NDIS_STATUS_PACKET_FILTER イベント GUID では、ミニポート アダプターのパケット フィルターの変更があったことを示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS は、パケット フィルターの構成の変更が存在する可能性を上にあるドライバーに通知する、NDIS_STATUS_PACKET_FILTER 状態を示す値を生成します。

NDIS は、WMI GUID_NDIS_STATUS_PACKET_FILTER イベントを WMI クライアントの状態表示を変換します。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900) ULONG 値が続く構造体。 パケット フィルターの状態と使用可能な値の詳細については、[OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md)を参照してください。

