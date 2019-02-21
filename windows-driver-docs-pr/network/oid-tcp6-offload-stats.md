---
title: OID_TCP6_OFFLOAD_STATS
description: このトピックでは、OID_TCP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: d7da8dd0-8de0-4283-9ecf-94e3d1503abe
keywords:
- OID_TCP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdfbe05f0f44c14d02d0b6abcb44961e28777cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559673"
---
# <a name="oidtcp6offloadstats"></a>OID_TCP6_OFFLOAD_STATS

ホストは、クエリ統計 IPv6 データグラムを伝達するオフロードの TCP 接続上で、オフロード対象が処理される TCP セグメントを作成する OID_TCP6_OFFLOAD_STATS OID をスタックします。 ホストのスタックは、この OID がゼロにこのような統計情報のカウンターをリセットする、オフロード対象を設定します。

OID_TCP6_OFFLOAD_STATS のクエリに応答してでは、オフロード対象を提供する入力で[TCP_OFFLOAD_STATS](https://msdn.microsoft.com/library/windows/hardware/ff570940)構造体。

OID_TCP6_OFFLOAD_STATS のセットへの応答をオフロード対象は、その IPv6 データグラムを伝達するオフロードの TCP 接続の TCP 統計カウンターのすべてをゼロにリセットする必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

