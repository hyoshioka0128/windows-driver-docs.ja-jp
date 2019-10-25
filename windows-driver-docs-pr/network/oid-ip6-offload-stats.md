---
title: OID_IP6_OFFLOAD_STATS
description: このトピックでは、OID_IP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 94bfc254-bc83-481f-a2d7-46c1e31e23a7
keywords:
- OID_IP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 240b63ee3acb94d5279f7e8c8aa372b39daa7aba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844593"
---
# <a name="oid_ip6_offload_stats"></a>OID_IP6_OFFLOAD_STATS

ホストスタックは OID_IP6_OFFLOAD_STATS OID に対してクエリを実行し、オフロードされた TCP 接続でオフロードターゲットが処理した IPv6 データグラムの統計を取得します。 ホストスタックはこの OID を設定して、オフロードターゲットがこのような統計のカウンターを0にリセットします。

OID_IP6_OFFLOAD_STATS のクエリに応答して、オフロードターゲットは、入力された[IP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ip_offload_stats)構造体を提供します。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続で処理される IPv6 データグラムの統計が含まれます。

OID_IP6_OFFLOAD_STATS のセットに対する応答として、オフロードターゲットは、すべての IPv6 統計カウンターをリセットし、TCP 接続をゼロに設定する必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

