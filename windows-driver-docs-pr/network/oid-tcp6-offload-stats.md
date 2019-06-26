---
title: OID_TCP6_OFFLOAD_STATS
description: このトピックでは、OID_TCP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: d7da8dd0-8de0-4283-9ecf-94e3d1503abe
keywords:
- OID_TCP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bb577faa7187bdb5f4b8861ea88f51cfc5c47fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353689"
---
# <a name="oidtcp6offloadstats"></a>OID_TCP6_OFFLOAD_STATS

ホストは、クエリ統計 IPv6 データグラムを伝達するオフロードの TCP 接続上で、オフロード対象が処理される TCP セグメントを作成する OID_TCP6_OFFLOAD_STATS OID をスタックします。 ホストのスタックは、この OID がゼロにこのような統計情報のカウンターをリセットする、オフロード対象を設定します。

OID_TCP6_OFFLOAD_STATS のクエリに応答してでは、オフロード対象を提供する入力で[TCP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_tcp_offload_stats)構造体。

OID_TCP6_OFFLOAD_STATS のセットへの応答をオフロード対象は、その IPv6 データグラムを伝達するオフロードの TCP 接続の TCP 統計カウンターのすべてをゼロにリセットする必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

