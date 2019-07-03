---
title: バグ チェック 0x16F CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP のバグ チェックでは、0x0000016F の値を持ちます。 これは、クラスターの共有ボリュームの次の状態遷移要求が到着していないことを示します。
keywords:
- バグ チェック 0x16F CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: da011b955643542b7eacad2aafd80b5f4088ace2
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519925"
---
# <a name="bug-check-0x16f-clustercsvstatetransitionintervaltimeoutlivedump"></a>バグ チェック 0x16F:クラスター\_CSV\_状態\_遷移\_間隔\_タイムアウト\_LIVEDUMP

クラスター\_CSV\_状態\_遷移\_間隔\_タイムアウト\_LIVEDUMP バグ チェックが 0x0000016F の値を持ちます。 これは、クラスターの共有ボリュームの次の状態遷移要求が到着していないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。



## <a name="clustercsvstatetransitionintervaltimeoutlivedump-parameters"></a>クラスター\_CSV\_状態\_遷移\_間隔\_タイムアウト\_LIVEDUMP パラメーター


|パラメーター|説明|
|--- |--- |
|1| サービスの PID をクラスターします。|
|2| CSV 対象の状態 Id - 以下にします。 |
|3| 予約済み |
|4| 予約済み |


**CSV 対象の状態 Id**

ボリュームの初期化状態に遷移するの 0 待機します。 

一時停止状態に移行するボリュームの 1 待機します。 

ドレイン中状態に移行するボリュームの 2 待機します。 

ダウン レベルの設定状態に移行するボリュームの 3 つの待機します。 

アクティブな状態に移行するボリュームの 4 待機します。

## <a name="cause"></a>原因
-----

クラスターの共有ボリュームの [次へ] の状態遷移要求が到着していません。

システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)


## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)
