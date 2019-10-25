---
title: GUID_NDIS_GEN_INTERRUPT_MODERATION
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_INTERRUPT_MODERATION GUID について説明します。
ms.assetid: 355e5e4d-61b7-4cc0-8cf7-c95a773e805a
keywords:
- GUID_NDIS_GEN_INTERRUPT_MODERATION、WDK GUID_NDIS_GEN_INTERRUPT_MODERATION ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fefb2170e984df25cc81133c35a9ba0c3ba900e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824273"
---
# <a name="guid_ndis_gen_interrupt_moderation"></a>GUID_NDIS_GEN_INTERRUPT_MODERATION

WMI クライアントは、GUID_NDIS_GEN_INTERRUPT_MODERATION メソッド GUID を使用して、ミニポートアダプターの指定したポートに関連付けられている割り込みモデレーションパラメーターを取得できます。

この GUID には、割り込みモデレーションパラメーターを返す WMI メソッド要求が必要です。 WMI メソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID であり、WMI 入力バッファーには[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。

NDIS は、この GUID を、関連付けられているミニポートアダプターの[OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md) query 要求に変換します。 この OID は、NDIS 6.0 以降のバージョンをサポートするミニポートドライバーに必須です。

NDIS によって GUID と共に返されるデータバッファーには、 [NDIS_INTERRUPT_MODERATION_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)構造体が含まれています。

ポートの状態の詳細については、「 [OID_GEN_INTERRUPT_MODERATION](oid-gen-interrupt-moderation.md)」を参照してください。

