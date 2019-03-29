---
title: バグ チェック 0x168 CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP のバグ チェックでは、0x00000168 の値を持ちます。 これは、クラスターの共有ボリュームの状態遷移時間がかかりすぎたことを示します。
keywords:
- バグ チェック 0x168 CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_STATE_TRANSITION_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06be642fd267715de8d712d81e9369d3d7f6d9e7
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743528"
---
# <a name="bug-check-0x168-clustercsvstatetransitiontimeoutlivedump"></a>バグ チェック 0x168 の。クラスター\_CSV\_状態\_遷移\_タイムアウト\_LIVEDUMP

クラスター\_CSV\_状態\_遷移\_タイムアウト\_LIVEDUMP バグ チェックが 0x00000168 の値を持ちます。 これは、クラスターの共有ボリュームの状態遷移時間がかかりすぎたことを示します。


**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="clustercsvstatetransitiontimeoutlivedump-parameters"></a>クラスター\_CSV\_状態\_遷移\_タイムアウト\_LIVEDUMP パラメーター

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

クラスターの共有ボリュームの状態遷移時間がかかりすぎました。 システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




