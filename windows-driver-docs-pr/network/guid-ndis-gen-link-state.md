---
title: GUID_NDIS_GEN_LINK_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_LINK_STATE について説明します。
ms.assetid: 0b0ebb57-33fb-4a18-b6e5-3f4300729280
keywords:
- GUID_NDIS_GEN_LINK_STATE、WDK GUID_NDIS_GEN_LINK_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6048b362463c2ca2bd8c01e4c4f4be74b4a611f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382709"
---
# <a name="guidndisgenlinkstate"></a>GUID_NDIS_GEN_LINK_STATE

WMI クライアントでは、現在のリンクの状態を判断するのに GUID_NDIS_GEN_LINK_STATE メソッド GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

WMI クライアント GUID_NDIS_GEN_LINK_STATE WMI メソッドの要求を発行と NDIS ミニポート アダプターまたは NDIS ポートの現在のリンクの状態を返します。

WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

この GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_LINK_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)構造体。

ミニポート ドライバーでは、初期化中に、リンクの状態を指定し、状態インジケーターの更新プログラムを提供します。 WMI クライアントでは、リンクの状態が変更されたときに、更新プログラムを受信するのに GUID_NDIS_GEN_LINK_STATE GUID を使用できます。

リンクのステータスの詳細については、次を参照してください。 [OID_GEN_LINK_STATE](oid-gen-link-state.md)と[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)します。

