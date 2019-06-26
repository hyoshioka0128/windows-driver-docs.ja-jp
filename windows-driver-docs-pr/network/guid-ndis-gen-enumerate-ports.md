---
title: GUID_NDIS_GEN_ENUMERATE_PORTS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_ENUMERATE_PORTS について説明します。
ms.assetid: c7572ff2-c9e1-4605-9768-b14636ce007f
keywords:
- GUID_NDIS_GEN_ENUMERATE_PORTS、WDK GUID_NDIS_GEN_ENUMERATE_PORTS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a2fddf9920673bb462b025d8d3f1c234d17568b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382742"
---
# <a name="guidndisgenenumerateports"></a>GUID_NDIS_GEN_ENUMERATE_PORTS

WMI クライアントでは、ミニポート アダプターに関連付けられているポートの一覧を取得するのに GUID GUID_NDIS_GEN_ENUMERATE_PORTS メソッドを使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS は、この要求を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID_NDIS_GEN_ENUMERATE_PORTS には、ポートを列挙する WMI メソッド要求が必要です。 WMI のメソッド識別子には、NDIS_WMI_DEFAULT_METHOD_ID 必要があります。 WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)ミニポート アダプタに対して NDIS ネットワーク インターフェイスの名前を識別する構造体、 **NetLuid**メンバーとする、0 を指定します、**PortNumber**メンバー。 WMI クライアントが取得できる、 **NetLuid**のアダプターの値、 [GUID_NDIS_ENUMERATE_ADAPTERS_EX](guid-ndis-enumerate-adapters-ex.md)メソッド GUID。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_PORT_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_array)構造体。 **NumberOfPorts** NDIS_PORT_ARRAY のメンバーには、ミニポート アダプターに関連付けられているアクティブなポートの数が含まれています。 **ポート**NDIS_PORT_ARRAY のメンバーにはへのポインターのリストが含まれています[NDIS_PORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)構造体。 各 NDIS_PORT_CHARACTERISTICS 構造体は、1 つの NDIS ポートの特性を定義します。

ポートの列挙の詳細については、次を参照してください。 [OID_GEN_ENUMERATE_PORTS](oid-gen-enumerate-ports.md)します。

