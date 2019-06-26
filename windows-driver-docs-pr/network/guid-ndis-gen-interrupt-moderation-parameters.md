---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS について説明します。
ms.assetid: f4be78b8-421b-467a-a0a6-b8256b8a4ab3
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS、WDK GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c84baf4c2e7aa4f1a6394e896331f00a772e6de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382727"
---
# <a name="guidndisgeninterruptmoderationparameters"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS

WMI クライアントでは、ミニポート アダプターの割り込みのモデレート構成を設定するのに GUID_NDIS_GEN_PORT_PARAMETERS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) OID を現在の構成を設定します。 すべての NDIS ミニポート ドライバーでは、この OID をサポートする必要があります。

WMI の入力バッファーが含まれています、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_set_header)が続く構造体、 [NDIS_INTERRUPT_MODERATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体。

ポート パラメーターの詳細については、次を参照してください。 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)します。

