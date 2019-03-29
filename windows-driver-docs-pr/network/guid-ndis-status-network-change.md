---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_NETWORK_CHANGE について説明します。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE、WDK GUID_NDIS_STATUS_NETWORK_CHANGE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05501d68bedf1ffbb3e366187154345adb3d51d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578088"
---
# <a name="guidndisstatusnetworkchange"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE イベント GUID では、レイヤー 3 のアドレスが再度ネゴシエートされることを示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS またはミニポート ドライバーが生成することができます、 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)ネットワークの状態の変更を報告する状態を示す値。

ミニポート ドライバーまたは NDIS は、ネットワークの状態の変化を示す、NDIS は WMI GUID_NDIS_STATUS_NETWORK_CHANGE イベントを WMI クライアントの状態表示を変換します。

この GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900) NDIS_NETWORK_CHANGE_TYPE 型の値が続く構造体。 使用可能な値については、次を参照してください。 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)します。

