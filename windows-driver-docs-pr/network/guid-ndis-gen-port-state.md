---
title: GUID_NDIS_GEN_PORT_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_PORT_STATE GUID について説明します。
ms.assetid: 0632843e-ea79-4ada-919e-8ab7d94a4421
keywords:
- GUID_NDIS_GEN_PORT_STATE、WDK GUID_NDIS_GEN_PORT_STATE ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52b9f26b121137ae183bddf8dabb6bfb54b4859
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842284"
---
# <a name="guid_ndis_gen_port_state"></a>GUID_NDIS_GEN_PORT_STATE

WMI クライアントは、GUID_NDIS_GEN_PORT_STATE メソッド GUID を使用して、NDIS ポートの状態を取得できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

GUID_NDIS_GEN_PORT_STATE では、NDIS ポートの状態を返す WMI メソッド要求が必要です。 WMI メソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID であり、WMI 入力バッファーには[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。

NDIS はこの GUID を処理し、ミニポートドライバーは OID クエリを受け取りません。

NDIS によって GUID と共に返されるデータバッファーには、 [NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)構造体が含まれています。

ポートの状態の詳細については、「 [OID_GEN_PORT_STATE](oid-gen-port-state.md)」を参照してください。

