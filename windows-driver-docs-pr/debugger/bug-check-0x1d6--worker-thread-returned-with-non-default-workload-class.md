---
title: バグ チェック 0x1D6 WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
description: WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS のバグ チェックでは、0x000001D6 の値を持ちます。 これは、ワーカー スレッドがそのワークロード クラスを変更し、戻る前に戻されませんでしたを示します。
keywords:
- バグ チェック 0x1D6 WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
- WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb2192c8a846c6d481e127f3b42a505c8b143741
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743590"
---
# <a name="bug-check-0x1d6-workerthreadreturnedwithnondefaultworkloadclass"></a>バグ チェック 0x1D6 の。ワーカー\_スレッド\_から返された\_WITH\_非\_既定\_ワークロード\_クラス

ワーカー\_スレッド\_から返された\_WITH\_非\_既定\_ワークロード\_クラスのバグ チェックが 0x000001D6 の値を持ちます。 これは、ワーカー スレッドがそのワークロード クラスを変更し、戻る前に戻されませんでしたを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

## <a name="workerthreadreturnedwithnondefaultworkloadclass-parameters"></a>ワーカー\_スレッド\_から返された\_WITH\_非\_既定\_ワークロード\_クラスのパラメーター

|パラメーター|説明|
|-------- |---------- |
|1| ワーカー ルーチン (責任のドライバーを検索するこの使用 ln) のアドレス |
|2| 現在のワークロード クラスの値。 |
|3| 作業項目のパラメーター。 |
|4| 作業項目のアドレス。 |

## <a name="cause"></a>原因
-----

ワーカー スレッドは、そのワークロード クラスを変更し、戻る前に戻されませんでした。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

