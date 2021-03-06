---
title: バグ チェック 0x16B CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
description: CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP のバグ チェックでは、0x0000016B の値を持ちます。 これは、クラスター サービスのユーザー モードのウォッチドッグでスレッドが長時間進行を行われていないことが検出されたことを示します。
keywords:
- バグ チェック 0x16B CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
- CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fe0db7ded38cf15bc86280ed8ef3775e50135a3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519946"
---
# <a name="bug-check-0x16b-clustercsvclusterwatchdoglivedump"></a>バグ チェック 0x16B:クラスター\_CSV\_クラスター\_ウォッチドッグ\_LIVEDUMP

クラスター\_CSV\_クラスター\_ウォッチドッグ\_LIVEDUMP バグ チェックが 0x0000016B の値を持ちます。 これは、クラスター サービスのユーザー モードのウォッチドッグでスレッドが長時間進行を行われていないことが検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。



## <a name="clustercsvclusterwatchdoglivedump-parameters"></a>クラスター\_CSV\_クラスター\_ウォッチドッグ\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| サービスの PID をクラスターします。|
|2| スタックしているスレッドの id。|
|3| 予約済み。|
|4| 予約済み。|

## <a name="cause"></a>原因
-----

クラスター サービスのユーザー モードのウォッチドッグは、スレッドが長時間進行を行われていないことが検出されました。

システムでは、遅延の分析のためのライブのダンプを生成します。

(このコード決してできますの実際のバグチェック。)

## <a name="resolution"></a>解決方法
----------
 

## <a name="see-also"></a>関連項目
----------

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




