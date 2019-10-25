---
title: GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES GUID について説明します。
ms.assetid: 5918fcb0-ebcf-4021-99a5-9ecfd2fdb987
keywords:
- GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES、WDK GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d16cb442881ebe9a7d28a6a9f4fc5992a81def
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842365"
---
# <a name="guid_ndis_tcp_offload_hw_capabilities"></a>GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES

WMI クライアントは、GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES メソッド GUID を使用して、ミニポートアダプターの指定したポートに関連付けられているハードウェアによってサポートされている TCP オフロード機能を取得できます。

この GUID には、NDIS ポートのハードウェア機能を返す WMI メソッド要求が必要です。 WMI メソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID であり、WMI 入力バッファーには[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。

NDIS はこの GUID を処理し、ミニポートドライバーは OID クエリを受け取りません。

NDIS によって GUID と共に返されるデータバッファーには、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)構造体が含まれています。

ポートの状態の詳細については、「 [OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)」を参照してください。

