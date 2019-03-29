---
title: OID_IP6_OFFLOAD_STATS
description: このトピックでは、OID_IP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 94bfc254-bc83-481f-a2d7-46c1e31e23a7
keywords:
- OID_IP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58affcd02f9bd3871e0f217808b74f5234b7de95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581291"
---
# <a name="oidip6offloadstats"></a>OID_IP6_OFFLOAD_STATS

ホストのスタックは、オフロードされた TCP 接続上で、オフロード対象が処理される IPv6 データグラムの統計情報を取得する OID_IP6_OFFLOAD_STATS OID を照会します。 ホストのスタックは、この OID がゼロにこのような統計情報のカウンターをリセットする、オフロード対象を設定します。

OID_IP6_OFFLOAD_STATS のクエリに応答してでは、オフロード対象を提供する入力で[IP_OFFLOAD_STATS](https://msdn.microsoft.com/library/windows/hardware/ff557022)構造体。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続上で処理された IPv6 データグラムの統計情報が含まれています。

OID_IP6_OFFLOAD_STATS のセットへの応答、オフロード対象はすべてゼロにオフロードされた TCP 接続の IPv6 の統計カウンターのリセットする必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

