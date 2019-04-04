---
title: GUID_NDIS_STATUS_OPER_STATUS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_OPER_STATUS について説明します。
ms.assetid: e4e13f9d-6298-47b0-9cb1-70fea87db59a
keywords:
- GUID_NDIS_STATUS_OPER_STATUS、WDK GUID_NDIS_STATUS_OPER_STATUS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63232d47b9f373c1588f748effb87e236071b68c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559341"
---
# <a name="guidndisstatusoperstatus"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS イベント GUID では、NDIS のネットワーク インターフェイスの現在の操作状態を示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS 生成、 [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md) NDIS のネットワーク インターフェイスの現在の操作状態を報告する状態を示す値。

NDIS は、NDIS のネットワーク インターフェイスの現在の操作状態の変更を示します、NDIS WMI GUID_NDIS_STATUS_OPER_STATUS イベントを WMI クライアントの状態の表示も変換されます。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)が続く構造体、 [NDIS_OPER_STATE](https://msdn.microsoft.com/library/windows/hardware/ff566737)構造体。 使用可能な値については、[NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)を参照してください。

