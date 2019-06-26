---
title: OID_TCP4_OFFLOAD_STATS
description: このトピックでは、OID_TCP4_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: e6933a86-0ff3-48ff-a0e3-3bfc32b19df3
keywords:
- OID_TCP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8f9809437d385555e02113006cced3145cf2e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353693"
---
# <a name="oidtcp4offloadstats"></a>OID_TCP4_OFFLOAD_STATS

ホストは、クエリ統計 IPv4 データグラムを伝達するオフロードの TCP 接続上で、オフロード対象が処理される TCP セグメントを作成する OID_TCP4_OFFLOAD_STATS OID をスタックします。 ホストのスタックは、この OID がゼロにこのような統計情報のカウンターをリセットする、オフロード対象を設定します。

OID_TCP4_OFFLOAD_STATS のクエリに応答してでは、オフロード対象を提供する入力で[TCP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_tcp_offload_stats)構造体。

OID_TCP4_OFFLOAD_STATS のセットへの応答、オフロード対象は、すべての IPv4 データグラムを伝えるオフロードの TCP 接続の TCP 統計カウンターをゼロにリセットする必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

