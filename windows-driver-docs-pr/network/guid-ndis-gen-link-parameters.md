---
title: GUID_NDIS_GEN_LINK_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_LINK_PARAMETERS GUID について説明します。
ms.assetid: 83895adf-2e66-4820-8037-52eb352b82fc
keywords:
- GUID_NDIS_GEN_LINK_PARAMETERS、WDK GUID_NDIS_GEN_LINK_PARAMETERS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 386d57b310ea340e582a1dcb2f87221e878589d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842290"
---
# <a name="guid_ndis_gen_link_parameters"></a>GUID_NDIS_GEN_LINK_PARAMETERS

WMI クライアントは、GUID_NDIS_GEN_LINK_PARAMETERS set GUID を使用して、ミニポートアダプターのリンクパラメーターを設定できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS は、この GUID を[OID_GEN_LINK_PARAMETERS](oid-gen-link-parameters.md) OID に変換して、ミニポートアダプターの現在のリンクパラメーターを設定します。 この OID は、NDIS 6.0 以降のバージョンをサポートするミニポートドライバーに必須です。

WMI 入力バッファーは、NDIS によって設定されるデータを指定します。 入力バッファーには、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)構造体の後に[NDIS_LINK_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-parameters)構造体が含まれています。

