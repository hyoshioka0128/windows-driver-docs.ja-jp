---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_LINK_PARAMETERS について説明します。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS、WDK GUID_NDIS_GEN_LINK_PARAMETERS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfeb8d1b7df18c08653adfd092260e9a8a286bad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537112"
---
# <a name="guidndisgenlinkparameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI クライアントでは、ミニポート アダプターのリンクのパラメーターを設定するのに GUID_NDIS_GEN_LINK_PARAMETERS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md)ミニポート アダプターの現在のリンクのパラメーターを設定する OID。 この OID は、NDIS 6.0 とそれ以降のバージョンをサポートするミニポート ドライバーに対して必須です。

WMI の入力バッファーには、NDIS を設定する必要がありますデータを指定します。 入力バッファーが含まれています、 [NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904)が続く構造体、 [NDIS_LINK_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff569592)構造体。

