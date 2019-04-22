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
ms.openlocfilehash: 80a06858183ca571bc5fafe2bf3802855a3a2ad1
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238481"
---
# <a name="bug-check-0x16b-clustercsvclusterwatchdoglivedump"></a>バグ チェック 0x16B:クラスター\_CSV\_クラスター\_ウォッチドッグ\_LIVEDUMP

クラスター\_CSV\_クラスター\_ウォッチドッグ\_LIVEDUMP バグ チェックが 0x0000016B の値を持ちます。 これは、クラスター サービスのユーザー モードのウォッチドッグでスレッドが長時間進行を行われていないことが検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。



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

[使用してライブ ダンプ (ブログ) のトラブルシューティングがハングします。](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[バグチェック コード リファレンス](bug-check-code-reference2.md)




