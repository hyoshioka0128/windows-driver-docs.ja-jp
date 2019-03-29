---
title: GUID_NDIS_STATUS_PORT_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_PORT_STATE について説明します。
ms.assetid: c657eef6-eb80-4715-9d60-0d2dde403300
keywords:
- GUID_NDIS_STATUS_PORT_STATE、WDK GUID_NDIS_STATUS_PORT_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd62de203e732d306abd348d1b67e535fc0c87d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580778"
---
# <a name="guidndisstatusportstate"></a>GUID_NDIS_STATUS_PORT_STATE

GUID_NDIS_STATUS_PORT_STATE イベント GUID では、NDIS ポートの状態の変更を示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS ポートの使用をサポートするミニポート ドライバー、 [NDIS_STATUS_PORT_STATE](ndis-status-port-state.md) NDIS ポートの状態の変化を示すステータスを示す値。

ミニポート ドライバーでは、ポートの状態が変更されたことを示します、NDIS は WMI GUID_NDIS_STATUS_PORT_STATE イベントを WMI クライアントの状態表示を変換します。

この GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)が続く構造体、 [NDIS_PORT_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569624)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_GEN_PORT_STATE](oid-gen-port-state.md)します。

