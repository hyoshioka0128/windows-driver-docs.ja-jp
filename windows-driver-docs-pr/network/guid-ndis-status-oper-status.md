---
title: GUID_NDIS_STATUS_OPER_STATUS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_OPER_STATUS について説明します。
ms.assetid: e4e13f9d-6298-47b0-9cb1-70fea87db59a
keywords:
- GUID_NDIS_STATUS_OPER_STATUS、WDK GUID_NDIS_STATUS_OPER_STATUS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbaaea0834a5bb2a0e04cf2860f16dc7e2c41aa1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369664"
---
# <a name="guidndisstatusoperstatus"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS イベント GUID では、NDIS のネットワーク インターフェイスの現在の操作状態を示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS 生成、 [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md) NDIS のネットワーク インターフェイスの現在の操作状態を報告する状態を示す値。

NDIS は、NDIS のネットワーク インターフェイスの現在の操作状態の変更を示します、NDIS WMI GUID_NDIS_STATUS_OPER_STATUS イベントを WMI クライアントの状態の表示も変換されます。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)が続く構造体、 [NDIS_OPER_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_oper_state)構造体。 使用可能な値については、次を参照してください。 [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)します。

