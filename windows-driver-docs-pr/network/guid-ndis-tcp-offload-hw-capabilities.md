---
title: GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES について説明します。
ms.assetid: 5918fcb0-ebcf-4021-99a5-9ecfd2fdb987
keywords:
- GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES、WDK GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55f558b55850ca7b5f1b328a04ee88bb41506d34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369634"
---
# <a name="guidndistcpoffloadhwcapabilities"></a>GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES

WMI クライアントでは、ミニポート アダプターの指定したポートに関連付けられているハードウェアでサポートされている TCP オフロード機能を取得するのに GUID GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES メソッドを使用できます。

この GUID は、NDIS ポートのハードウェア機能を返す WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)します。

