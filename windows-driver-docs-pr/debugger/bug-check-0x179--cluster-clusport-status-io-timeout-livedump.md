---
title: バグ チェック 0x179 CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
description: CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP のバグ チェックでは、0x00000179 の値を持ちます。 これは、イニシエーターのノード上の SMB クライアントがターゲット ノードで IO が時間がかかりすぎると、STATUS_IO_TIMEOUT ですべての IOs が失敗したという苦情することを示します。
keywords:
- バグ チェック 0x179 CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
- CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa1d96f00ba7ac61a9b63208be9a20bd3a1e04e6
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519889"
---
# <a name="bug-check-0x179-clusterclusportstatusiotimeoutlivedump"></a>バグ チェック 0x179:クラスター\_CLUSPORT\_状態\_IO\_タイムアウト\_LIVEDUMP

クラスター\_CLUSPORT\_状態\_IO\_タイムアウト\_LIVEDUMP バグ チェックが 0x00000179 の値を持ちます。 これは、イニシエーターのノード上の SMB クライアントがターゲット ノードに IO は時間がかかりすぎると、STATUS_IO_TIMEOUT ですべての IOs が失敗したという苦情することを示します。



> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。



## <a name="clusterclusportstatusiotimeoutlivedump-parameters"></a>クラスター\_CLUSPORT\_状態\_IO\_タイムアウト\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--------------- |
|1| タイムアウトに IRP します。|
|2| 予約済み。 |
|3| 予約済み。 |
|4| 予約済み。 |


## <a name="cause"></a>原因
-----

イニシエーターのノード上の SMB クライアントは、ターゲット ノードで IO が時間がかかりすぎると、STATUS_IO_TIMEOUT ですべての IOs が失敗したという苦情います。

それに対応、何 IO 時間がかかる状況を分析するため、クラスター イニシエーターはイニシエーターのノードにライブのダンプをキャプチャします。

追加情報は、ダンプのセカンダリのデータ ストリームで使用できます。

(このコード決してできますの実際のバグチェック。)


## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




