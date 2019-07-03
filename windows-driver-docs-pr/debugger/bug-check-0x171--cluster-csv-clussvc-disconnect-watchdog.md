---
title: バグ チェック 0x171 CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
description: CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG のバグ チェックでは、0x00000171 の値を持ちます。 これは、クラスターの切断によって進行が行われていないことを示します。
keywords:
- バグ チェック 0x171 CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
- CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8615654173f804d4aca5a9e4970d38d8e62255dd
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519919"
---
# <a name="bug-check-0x171-clustercsvclussvcdisconnectwatchdog"></a>バグ チェック 0x171:クラスター\_CSV\_CLUSSVC\_切断\_ウォッチドッグ

クラスター\_CSV\_CLUSSVC\_切断\_ウォッチドッグのバグ チェックが 0x00000171 の値を持ちます。 これは、クラスターの切断によって進行が行われていないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。



## <a name="clustercsvclussvcdisconnectwatchdog-parameters"></a>クラスター\_CSV\_CLUSSVC\_切断\_ウォッチドッグ パラメーター

|パラメーター|説明|
|--- |--- |
|1| クラスターの切断を処理しているスレッドの id。|
|2| タイムアウト (ミリ秒単位)。 |
|3| 予約済み |
|4| 予約済み |

## <a name="cause"></a>原因
-----

クラスターの切断が進行をしていません。


## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




