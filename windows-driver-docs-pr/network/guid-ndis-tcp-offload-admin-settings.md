---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS について説明します。
ms.assetid: 8648c75a-dcb3-4723-a2d0-d406d3a073d6
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS、WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 702cc30eb8ba56c7b82406205f262e758839e59b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369653"
---
# <a name="guidndistcpoffloadadminsettings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI クライアントでは、オフロードは、NDIS ポートの構成パラメーターを設定するのに GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) NDIS ポートの現在の構成を設定する OID。 タスク オフロードの任意の種類のサポートを提供する NDIS ミニポート ドライバーでは、この OID をサポートする必要があります。

WMI の入力バッファーが含まれています、 [NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_set_header)が続く構造体、 [NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)構造体。

ポート パラメーターの詳細については、次を参照してください。 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)します。

