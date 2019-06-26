---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_INTERRUPT_MODERATION について説明します。
ms.assetid: 355e5e4d-61b7-4cc0-8cf7-c95a773e805a
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION、WDK GUID_NDIS_GEN_INTERRUPT_MODERATION ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd2f935ec3884c7ea12642439d645cea6fb02b39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382725"
---
# <a name="guidndisgeninterruptmoderation"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION

WMI クライアントでは、パラメーターを取得、割り込み節度ミニポート アダプターの指定したポートに関連付けられている GUID GUID_NDIS_GEN_INTERRUPT_MODERATION メソッドを使用できます。

この GUID は、割り込みのモデレート パラメーターを取得する WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

NDIS に変換するには、この GUID を[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)クエリ要求に関連付けられているミニポート アダプター。 この OID は、NDIS 6.0 とそれ以降のバージョンをサポートするミニポート ドライバーに対して必須です。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_INTERRUPT_MODERATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)します。

