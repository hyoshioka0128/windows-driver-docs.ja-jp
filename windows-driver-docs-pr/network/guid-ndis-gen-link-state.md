---
title: GUID_NDIS_GEN_LINK_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_LINK_STATE GUID について説明します。
ms.assetid: 0b0ebb57-33fb-4a18-b6e5-3f4300729280
keywords:
- GUID_NDIS_GEN_LINK_STATE、WDK GUID_NDIS_GEN_LINK_STATE ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: af7d1dd054ad9c0468c623a2916bf05a2a43fa02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842289"
---
# <a name="guid_ndis_gen_link_state"></a>GUID_NDIS_GEN_LINK_STATE

WMI クライアントは、GUID_NDIS_GEN_LINK_STATE メソッド GUID を使用して、現在のリンクの状態を確認できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

NDIS では、この GUID とミニポートドライバーは OID クエリを受け取りません。

WMI クライアントが GUID_NDIS_GEN_LINK_STATE WMI メソッド要求を発行すると、NDIS はミニポートアダプターまたは NDIS ポートの現在のリンクの状態を返します。

WMI メソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID であり、WMI 入力バッファーには[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。

この GUID で NDIS が返すデータバッファーには、 [NDIS_LINK_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)構造体が含まれています。

ミニポートドライバーは、初期化中にリンク状態を提供し、状態を示す更新プログラムを提供します。 WMI クライアントは、GUID_NDIS_GEN_LINK_STATE GUID を使用して、リンクの状態が変化したときに更新プログラムを受け取ることができます。

リンクステータスの詳細については、「 [OID_GEN_LINK_STATE](oid-gen-link-state.md) and [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)」を参照してください。

