---
title: OID_TCP6_OFFLOAD_STATS
description: このトピックでは、OID_TCP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: d7da8dd0-8de0-4283-9ecf-94e3d1503abe
keywords:
- OID_TCP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6199126ca4fc008dd70257d4af711e9202a4f7d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843877"
---
# <a name="oid_tcp6_offload_stats"></a>OID_TCP6_OFFLOAD_STATS

ホストスタックは OID_TCP6_OFFLOAD_STATS OID に対してクエリを実行し、オフロードターゲットが、IPv6 データグラムを伝達するオフロード TCP 接続で処理された TCP セグメントの統計情報を取得します。 ホストスタックはこの OID を設定して、オフロードターゲットがこのような統計のカウンターを0にリセットします。

OID_TCP6_OFFLOAD_STATS のクエリに応答して、オフロードターゲットは、入力された[TCP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_tcp_offload_stats)構造体を提供します。

OID_TCP6_OFFLOAD_STATS のセットに対する応答として、オフロードターゲットは、IPv6 データグラムを伝達するオフロード TCP 接続のすべての TCP 統計カウンターを0にリセットする必要があります。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

