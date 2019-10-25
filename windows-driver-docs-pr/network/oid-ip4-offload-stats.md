---
title: OID_IP4_OFFLOAD_STATS
description: このトピックでは、OID_IP4_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 7ffe9703-5370-410f-bccd-4a430835edd0
keywords:
- OID_IP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e1a685714554d8e28692ebaf5e191a2acb91de3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844589"
---
# <a name="oid_ip4_offload_stats"></a>OID_IP4_OFFLOAD_STATS

ホストスタックは OID_IP4_OFFLOAD_STATS OID に対してクエリを実行し、オフロードされた TCP 接続でオフロードターゲットが処理した IPv4 データグラムの統計情報を取得します。 ホストスタックはこの OID を設定して、オフロードターゲットがこのような統計のカウンターを0にリセットします。

OID_IP4_OFFLOAD_STATS のクエリに応答して、オフロードターゲットは、入力された[IP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ip_offload_stats)構造体を提供します。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続で処理された IPv4 データグラムの統計が含まれます。

OID_IP4_OFFLOAD_STATS のセットに対する応答として、オフロードターゲットは、オフロードされた TCP 接続のすべての IPv4 統計カウンターを0にリセットする必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

