---
title: GUID_NDIS_GEN_ENUMERATE_PORTS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_ENUMERATE_PORTS GUID について説明します。
ms.assetid: c7572ff2-c9e1-4605-9768-b14636ce007f
keywords:
- GUID_NDIS_GEN_ENUMERATE_PORTS、WDK GUID_NDIS_GEN_ENUMERATE_PORTS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f20b3ca8a4d773e90663730f1f8d1602b7983e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842178"
---
# <a name="guid_ndis_gen_enumerate_ports"></a>GUID_NDIS_GEN_ENUMERATE_PORTS

WMI クライアントは、GUID_NDIS_GEN_ENUMERATE_PORTS メソッド GUID を使用して、ミニポートアダプターに関連付けられているポートの一覧を取得できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS はこの要求を処理し、ミニポートドライバーは OID クエリを受け取りません。

GUID_NDIS_GEN_ENUMERATE_PORTS には、ポートを列挙するための WMI メソッド要求が必要です。 WMI メソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID にする必要があります。 WMI 入力バッファーには、 **Netluid**メンバーのミニポートアダプターの NDIS ネットワークインターフェイス名を識別する[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。これ**は、ポート番号メンバーに**ゼロを指定します。 WMI クライアントは、 [GUID_NDIS_ENUMERATE_ADAPTERS_EX](guid-ndis-enumerate-adapters-ex.md)メソッド GUID を使用して、アダプターの**netluid**値を取得できます。

NDIS によって GUID と共に返されるデータバッファーには、 [NDIS_PORT_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)構造体が含まれています。 NDIS_PORT_ARRAY の**Numberofports**メンバーには、ミニポートアダプターに関連付けられているアクティブなポートの数が含まれています。 NDIS_PORT_ARRAY の**Ports**メンバーには、 [NDIS_PORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造体へのポインターの一覧が含まれています。 各 NDIS_PORT_CHARACTERISTICS 構造体は、1つの NDIS ポートの特性を定義します。

ポートの列挙の詳細については、「 [OID_GEN_ENUMERATE_PORTS](oid-gen-enumerate-ports.md)」を参照してください。

