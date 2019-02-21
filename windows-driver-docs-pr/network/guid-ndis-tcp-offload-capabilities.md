---
title: GUID_NDIS_TCP_OFFLOAD_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_TCP_OFFLOAD_CAPABILITIES について説明します。
ms.assetid: 93b8af60-3c15-4eea-a0ea-ce1c71f0b60c
keywords:
- GUID_NDIS_TCP_OFFLOAD_CAPABILITIES、WDK GUID_NDIS_TCP_OFFLOAD_CAPABILITIES ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: da07d5f3c65a0eb4e9d51b849c3c6c13789d0367
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532516"
---
# <a name="guidndistcpoffloadcapabilities"></a>GUID_NDIS_TCP_OFFLOAD_CAPABILITIES

WMI クライアントでは、オフロード機能ミニポート アダプターの指定したポートに関連付けられているタスクを取得するのに GUID GUID_NDIS_TCP_OFFLOAD_CAPABILITIES メソッドを使用できます。

この GUID は、NDIS ポートのオフロード機能を返す WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)構造体。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)します。

