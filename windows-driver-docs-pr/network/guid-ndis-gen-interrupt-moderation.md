---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_INTERRUPT_MODERATION について説明します。
ms.assetid: 355e5e4d-61b7-4cc0-8cf7-c95a773e805a
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION、WDK GUID_NDIS_GEN_INTERRUPT_MODERATION ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 057195bdfcd75360932da994c844d42767fd11a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529071"
---
# <a name="guidndisgeninterruptmoderation"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION

WMI クライアントでは、パラメーターを取得、割り込み節度ミニポート アダプターの指定したポートに関連付けられている GUID GUID_NDIS_GEN_INTERRUPT_MODERATION メソッドを使用できます。

この GUID は、割り込みのモデレート パラメーターを取得する WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)構造体。

NDIS に変換するには、この GUID を[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)クエリ要求に関連付けられているミニポート アダプター。 この OID は、NDIS 6.0 とそれ以降のバージョンをサポートするミニポート ドライバーに対して必須です。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_INTERRUPT_MODERATION_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff565793)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)します。

