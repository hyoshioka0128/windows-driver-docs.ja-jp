---
title: GUID_NDIS_TCP_OFFLOAD_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_TCP_OFFLOAD_CAPABILITIES について説明します。
ms.assetid: 93b8af60-3c15-4eea-a0ea-ce1c71f0b60c
keywords:
- GUID_NDIS_TCP_OFFLOAD_CAPABILITIES、WDK GUID_NDIS_TCP_OFFLOAD_CAPABILITIES ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86208084d85be1f9be2e89b4ab44b794a0d3a7cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355122"
---
# <a name="guidndistcpoffloadcapabilities"></a>GUID_NDIS_TCP_OFFLOAD_CAPABILITIES

WMI クライアントでは、オフロード機能ミニポート アダプターの指定したポートに関連付けられているタスクを取得するのに GUID GUID_NDIS_TCP_OFFLOAD_CAPABILITIES メソッドを使用できます。

この GUID は、NDIS ポートのオフロード機能を返す WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)します。

