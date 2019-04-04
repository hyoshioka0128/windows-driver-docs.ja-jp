---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS について説明します。
ms.assetid: f4be78b8-421b-467a-a0a6-b8256b8a4ab3
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS、WDK GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb2583d2fba0b86f7f1d76700657055de19c9cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537117"
---
# <a name="guidndisgeninterruptmoderationparameters"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS

WMI クライアントでは、ミニポート アダプターの割り込みのモデレート構成を設定するのに GUID_NDIS_GEN_PORT_PARAMETERS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) OID を現在の構成を設定します。 すべての NDIS ミニポート ドライバーでは、この OID をサポートする必要があります。

WMI の入力バッファーが含まれています、 [NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904)が続く構造体、 [NDIS_INTERRUPT_MODERATION_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff565793)構造体。

ポート パラメーターの詳細については、[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)を参照してください。

