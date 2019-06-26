---
title: GUID_NDIS_GEN_PORT_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_PORT_STATE について説明します。
ms.assetid: 0632843e-ea79-4ada-919e-8ab7d94a4421
keywords:
- GUID_NDIS_GEN_PORT_STATE、WDK GUID_NDIS_GEN_PORT_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7c7b3f98eadbe8ed0002fe41a543fd4f250324
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382702"
---
# <a name="guidndisgenportstate"></a>GUID_NDIS_GEN_PORT_STATE

WMI クライアントでは、NDIS ポートの状態を取得するのに GUID GUID_NDIS_GEN_PORT_STATE メソッドを使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

GUID_NDIS_GEN_PORT_STATE では、NDIS ポートの状態を返す WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_GEN_PORT_STATE](oid-gen-port-state.md)します。

