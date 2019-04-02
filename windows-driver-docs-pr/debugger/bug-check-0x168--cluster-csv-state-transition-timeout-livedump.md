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
ms.openlocfilehash: 7875bf4fb6e58cce425c5f0dd4d943b26e554706
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761849"
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

ボリュームの初期化状態に遷移するの 0 待機します。 

一時停止状態に移行するボリュームの 1 待機します。 

ドレイン中状態に移行するボリュームの 2 待機します。 

ダウン レベルの設定状態に移行するボリュームの 3 つの待機します。 

アクティブな状態に移行するボリュームの 4 待機します。


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




