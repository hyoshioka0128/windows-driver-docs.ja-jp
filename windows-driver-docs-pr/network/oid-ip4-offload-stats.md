---
title: OID_IP4_OFFLOAD_STATS
description: このトピックでは、OID_IP4_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 7ffe9703-5370-410f-bccd-4a430835edd0
keywords:
- OID_IP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007f394ab414856333a32a20b85b3d3145b70cf8
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916788"
---
# <a name="oid_ip4_offload_stats"></a>OID_IP4_OFFLOAD_STATS

ホストスタックは、オフロードされた TCP 接続でオフロードターゲットが処理した IPv4 データグラムの統計を取得するために、OID_IP4_OFFLOAD_STATS OID を照会します。 ホストスタックはこの OID を設定して、オフロードターゲットがこのような統計のカウンターを0にリセットします。

OID_IP4_OFFLOAD_STATS のクエリに応答して、オフロードターゲットは、入力された[IP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ip_offload_stats)構造を提供します。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続で処理される IPv4 データグラムの統計が含まれます。

オフロードターゲットは、一連の OID_IP4_OFFLOAD_STATS に応答して、オフロードされた TCP 接続のすべての IPv4 統計カウンターを0にリセットする必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

