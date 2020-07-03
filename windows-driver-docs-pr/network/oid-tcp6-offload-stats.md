---
title: OID_TCP6_OFFLOAD_STATS
description: このトピックでは、OID_TCP6_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: d7da8dd0-8de0-4283-9ecf-94e3d1503abe
keywords:
- OID_TCP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2b8645a264c8d6421998774c25f938c20820837
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917134"
---
# <a name="oid_tcp6_offload_stats"></a>OID_TCP6_OFFLOAD_STATS

ホストスタックは、OID_TCP6_OFFLOAD_STATS OID を照会して、オフロードターゲットが、IPv6 データグラムを伝達するオフロードされた TCP 接続で処理されたことを示す TCP セグメントの統計情報を取得します。 ホストスタックはこの OID を設定して、オフロードターゲットがこのような統計のカウンターを0にリセットします。

OID_TCP6_OFFLOAD_STATS のクエリに応答して、オフロードターゲットは、入力された[TCP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_tcp_offload_stats)構造を提供します。

一連の OID_TCP6_OFFLOAD_STATS に対する応答として、オフロードターゲットは、IPv6 データグラムを伝達するオフロード TCP 接続のすべての TCP 統計カウンターを0にリセットする必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

