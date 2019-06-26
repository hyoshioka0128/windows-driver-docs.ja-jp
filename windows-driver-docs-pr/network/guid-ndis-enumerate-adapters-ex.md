---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_ENUMERATE_ADAPTERS_EX について説明します。
ms.assetid: 46c4c127-a9f6-4555-82d1-3c537fbb7914
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX、WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b1040804dffdd7e79b08e4ef22944a7cd9d4fdb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382731"
---
# <a name="guidndisenumerateadaptersex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI クライアントでは、すべてのコンピューターのミニポート アダプタの列挙体を取得するのに GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。 NDIS は、すべての読み込まれたミニポート アダプターを追跡しているため、NDIS はこの情報のミニポート ドライバーをクエリできません。

WMI クライアントは、この GUID を使用してデバイス名と関連付けられている値を検索することができます、 **NetLuid**のメンバー、 [NDIS_WMI_ENUM_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_enum_adapter)構造体。 WMI クライアントが使用できる、 **NetLuid**アダプターは、GUID の後続の要求の値。

GUID を持つ NDIS が返すデータ バッファーには、NDIS_WMI_ENUM_ADAPTER 構造体の配列が含まれています。

