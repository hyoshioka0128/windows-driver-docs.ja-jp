---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS GUID について説明します。
ms.assetid: f4be78b8-421b-467a-a0a6-b8256b8a4ab3
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS、WDK GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24dfd38679bda5bdf09a93a6139a749b8aa6150d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842175"
---
# <a name="guid_ndis_gen_interrupt_moderation_parameters"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION_PARAMETERS

WMI クライアントは、GUID_NDIS_GEN_PORT_PARAMETERS set GUID を使用して、ミニポートアダプターの割り込みモデレーション構成を設定できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS は、この GUID を[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) OID に変換し、現在の構成を設定します。 すべての NDIS ミニポートドライバーは、この OID をサポートする必要があります。

WMI 入力バッファーには、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)構造体の後に[NDIS_INTERRUPT_MODERATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体が含まれています。

ポートパラメーターの詳細については、「 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)」を参照してください。

