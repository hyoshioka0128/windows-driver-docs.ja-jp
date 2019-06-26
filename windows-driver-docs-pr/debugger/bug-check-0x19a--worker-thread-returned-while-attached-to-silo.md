---
title: バグ チェック 0x19A WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
description: WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO のバグ チェックでは、0x0000019A の値を持ちます。 これは、ワーカー スレッドが、サイロにアタッチし、戻る前にデタッチできませんでしたを示します。
ms.assetid: D947FF20-4C86-4879-A5CA-934A20BE61C9
keywords:
- バグ チェック 0x19A WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
- WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1d83804980e78c8f749fef3787df9e27032806a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367650"
---
# <a name="bug-check-0x19a-workerthreadreturnedwhileattachedtosilo"></a>バグ チェック 0x19A:ワーカー\_スレッド\_から返された\_中\_ATTACHED\_TO\_サイロ


ワーカー\_スレッド\_から返された\_中\_ATTACHED\_TO\_サイロのバグ チェックが 0x0000019A の値を持ちます。 これは、ワーカー スレッドが、サイロにアタッチし、戻る前にデタッチできませんでしたを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="workerthreadreturnedwhileattachedtosilo-parameters"></a>ワーカー\_スレッド\_から返された\_中\_ATTACHED\_TO\_サイロ パラメーター


| パラメーター | 説明               |
|-----------|---------------------------|
| 1         | ワーカーのルーチンのアドレス |
| 2         | 作業項目のパラメーター        |
| 3         | 作業項目のアドレス          |
| 4         | 予約済み                  |

 

<a name="cause"></a>原因
-----

使用を調査するために、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)コマンドをパラメーター 1 が正しく動作のドライバーを識別できるようにします。

 

 




