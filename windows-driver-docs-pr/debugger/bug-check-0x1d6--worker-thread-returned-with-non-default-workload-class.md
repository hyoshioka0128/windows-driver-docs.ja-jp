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
ms.openlocfilehash: e7c3a0e5a80475c9213ba58f8a22fbaa6480b3cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361619"
---
# <a name="bug-check-0x1d6-workerthreadreturnedwithnondefaultworkloadclass"></a>バグ チェック 0x1D6:ワーカー\_スレッド\_から返された\_WITH\_非\_既定\_ワークロード\_クラス

ワーカー\_スレッド\_から返された\_WITH\_非\_既定\_ワークロード\_クラスのバグ チェックが 0x000001D6 の値を持ちます。 これは、ワーカー スレッドがそのワークロード クラスを変更し、戻る前に戻されませんでしたを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

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

