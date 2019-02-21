---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_ENUMERATE_ADAPTERS_EX について説明します。
ms.assetid: 46c4c127-a9f6-4555-82d1-3c537fbb7914
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX、WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2b2de5dc51bfe03cb14ecc173e83dee3f8556f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559928"
---
# <a name="guidndisenumerateadaptersex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI クライアントでは、すべてのコンピューターのミニポート アダプタの列挙体を取得するのに GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。 NDIS は、すべての読み込まれたミニポート アダプターを追跡しているため、NDIS はこの情報のミニポート ドライバーをクエリできません。

WMI クライアントは、この GUID を使用してデバイス名と関連付けられている値を検索することができます、 **NetLuid**のメンバー、 [NDIS_WMI_ENUM_ADAPTER](https://msdn.microsoft.com/library/windows/hardware/ff567899)構造体。 WMI クライアントが使用できる、 **NetLuid**アダプターは、GUID の後続の要求の値。

GUID を持つ NDIS が返すデータ バッファーには、NDIS_WMI_ENUM_ADAPTER 構造体の配列が含まれています。

