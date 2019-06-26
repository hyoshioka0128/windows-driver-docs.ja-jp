---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_LINK_PARAMETERS について説明します。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS、WDK GUID_NDIS_GEN_LINK_PARAMETERS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b1b23c86fd8f61c775632e8301d885d7fbf569c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382719"
---
# <a name="guidndisgenlinkparameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI クライアントでは、ミニポート アダプターのリンクのパラメーターを設定するのに GUID_NDIS_GEN_LINK_PARAMETERS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md)ミニポート アダプターの現在のリンクのパラメーターを設定する OID。 この OID は、NDIS 6.0 とそれ以降のバージョンをサポートするミニポート ドライバーに対して必須です。

WMI の入力バッファーには、NDIS を設定する必要がありますデータを指定します。 入力バッファーが含まれています、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_set_header)が続く構造体、 [NDIS_LINK_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-parameters)構造体。

