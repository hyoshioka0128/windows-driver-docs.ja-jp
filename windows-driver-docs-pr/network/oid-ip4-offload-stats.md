---
title: OID_IP4_OFFLOAD_STATS
description: このトピックでは、OID_IP4_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 7ffe9703-5370-410f-bccd-4a430835edd0
keywords:
- OID_IP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7354a7f963d634843e665f0300d6b15d488337dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385730"
---
# <a name="oidip4offloadstats"></a>OID_IP4_OFFLOAD_STATS

ホストのスタックは、オフロードされた TCP 接続上で、オフロード対象が処理される IPv4 データグラムの統計情報を取得する OID_IP4_OFFLOAD_STATS OID を照会します。 ホストのスタックは、この OID がゼロにこのような統計情報のカウンターをリセットする、オフロード対象を設定します。

OID_IP4_OFFLOAD_STATS のクエリに応答してでは、オフロード対象を提供する入力で[IP_OFFLOAD_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ip_offload_stats)構造体。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続上で処理された IPv4 データグラムの統計情報が含まれています。

OID_IP4_OFFLOAD_STATS のセットへの応答、オフロード対象が、すべてのゼロにオフロードの TCP 接続をその IPv4 statistics カウンターをリセットする必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

