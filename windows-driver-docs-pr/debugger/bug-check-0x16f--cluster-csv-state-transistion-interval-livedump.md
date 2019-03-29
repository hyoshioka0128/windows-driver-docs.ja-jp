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
ms.openlocfilehash: 135a66a5a7933e8bda6cae8c34bad6757be286a4
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743573"
---
# <a name="bug-check-0x16f-clustercsvstatetransitionintervaltimeoutlivedump"></a>バグ チェック 0x16F の。クラスター\_CSV\_状態\_遷移\_間隔\_タイムアウト\_LIVEDUMP

クラスター\_CSV\_状態\_遷移\_間隔\_タイムアウト\_LIVEDUMP バグ チェックが 0x0000016F の値を持ちます。 これは、クラスターの共有ボリュームの次の状態遷移要求が到着していないことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="clustercsvstatetransitionintervaltimeoutlivedump-parameters"></a>クラスター\_CSV\_状態\_遷移\_間隔\_タイムアウト\_LIVEDUMP パラメーター


|パラメーター|説明|
|--- |--- |
|1| サービスの PID をクラスターします。|
|2| CSV 対象の状態 Id - 以下にします。 |
|3| 予約済み |
|4| 予約済み |


**CSV 対象の状態 Id**

     0  Waiting for volume to transition to the Init state. 
     1  Waiting for volume to transition to the Paused state. 
     2  Waiting for volume to transition to the Draining state. 
     3  Waiting for volume to transition to the Set-Down-Level state. 
     4  Waiting for volume to transition to the Active state.


## <a name="cause"></a>原因
-----

クラスターの共有ボリュームの [次へ] の状態遷移要求が到着していません。

システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)


## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




