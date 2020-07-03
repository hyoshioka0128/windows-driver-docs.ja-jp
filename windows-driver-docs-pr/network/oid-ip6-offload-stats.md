---
title: OID_IP6_OFFLOAD_STATS
description: このトピックでは、OID_IP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 94bfc254-bc83-481f-a2d7-46c1e31e23a7
keywords:
- OID_IP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe4e5c276a35481bc31feab0d21fc7de63047493
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916095"
---
# <a name="oid_ip6_offload_stats"></a>OID_IP6_OFFLOAD_STATS

ホストスタックは、オフロードされた TCP 接続でオフロードターゲットが処理した IPv6 データグラムの統計を取得するために、OID_IP6_OFFLOAD_STATS OID に対してクエリを実行します。 ホストスタックはこの OID を設定して、オフロードターゲットがこのような統計のカウンターを0にリセットします。

OID_IP6_OFFLOAD_STATS のクエリに応答して、オフロードターゲットは、入力された[IP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ip_offload_stats)構造を提供します。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続で処理される IPv6 データグラムの統計が含まれます。

オフロードターゲットは、一連の OID_IP6_OFFLOAD_STATS に応答して、オフロードされた TCP 接続のすべての IPv6 統計カウンターを0にリセットする必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

