---
title: OID_IP4_OFFLOAD_STATS
description: このトピックでは、OID_IP4_OFFLOAD_STATS オブジェクト識別子 (OID) について説明します。
ms.assetid: 7ffe9703-5370-410f-bccd-4a430835edd0
keywords:
- OID_IP4_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5570371564eb2273c74cd6c941c9812ed6862c10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354177"
---
# <a name="oidip4offloadstats"></a>OID_IP4_OFFLOAD_STATS

ホストのスタックは、オフロードされた TCP 接続上で、オフロード対象が処理される IPv4 データグラムの統計情報を取得する OID_IP4_OFFLOAD_STATS OID を照会します。 ホストのスタックは、この OID がゼロにこのような統計情報のカウンターをリセットする、オフロード対象を設定します。

OID_IP4_OFFLOAD_STATS のクエリに応答してでは、オフロード対象を提供する入力で[IP_OFFLOAD_STATS](https://msdn.microsoft.com/library/windows/hardware/ff557022)構造体。 IP_OFFLOAD_STATS 構造体には、オフロードされた TCP 接続上で処理された IPv4 データグラムの統計情報が含まれています。

OID_IP4_OFFLOAD_STATS のセットへの応答、オフロード対象が、すべてのゼロにオフロードの TCP 接続をその IPv4 statistics カウンターをリセットする必要があります。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

