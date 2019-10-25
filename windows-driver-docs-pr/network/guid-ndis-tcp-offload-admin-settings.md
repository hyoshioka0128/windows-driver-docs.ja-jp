---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS GUID について説明します。
ms.assetid: 8648c75a-dcb3-4723-a2d0-d406d3a073d6
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS、WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: a88c41b345605a04d8713ba2a58ad0142eae29e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842369"
---
# <a name="guid_ndis_tcp_offload_admin_settings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI クライアントは、GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS set GUID を使用して、NDIS ポートのオフロード構成パラメーターを設定できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS は、この GUID を[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID に変換して、ndis ポートの現在の構成を設定します。 タスクオフロードのあらゆる種類のサポートを提供する NDIS ミニポートドライバーは、この OID をサポートする必要があります。

WMI 入力バッファーには、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)構造体の後に[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体が含まれています。

ポートパラメーターの詳細については、「 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)」を参照してください。

