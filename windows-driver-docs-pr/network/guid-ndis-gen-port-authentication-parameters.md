---
title: GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS GUID について説明します。
ms.assetid: a61e972b-0969-4ee8-ad57-cf88beda962d
keywords:
- GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS、WDK GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: bafa1462bd4fc019be73119e71246eeb5d626d44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842286"
---
# <a name="guid_ndis_gen_port_authentication_parameters"></a>GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS

WMI クライアントは、GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS set GUID を使用して、NDIS ポートのポート認証パラメーターを設定できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS は、この GUID を[OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md) OID に変換して、ndis ポートの現在の認証構成を設定します。 NDIS ポートをサポートするミニポートドライバーは、この OID をサポートする必要があります。

WMI 入力バッファーでは、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)構造体の後に NDIS_PORT_AUTHENTICATION_PARAMETERS 構造体が指定されています。

ポートパラメーターの詳細については、「 [OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md)」を参照してください。

