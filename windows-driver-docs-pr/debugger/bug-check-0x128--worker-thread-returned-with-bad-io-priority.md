---
title: Bug Check 0x128 WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
description: WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY のバグ チェックでは、0x00000128 の値を持ちます。 これは、ワーカー スレッド IOPriority が呼び出されるワーカー ルーチンによって誤って変更されたことを示します。
ms.assetid: 2659491F-2257-4553-A7A4-ECA39DD0A0F7
keywords:
- Bug Check 0x128 WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
- WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0f0d852cdef58edbe655535fef4cb0f46477b120
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520704"
---
# <a name="bug-check-0x128-workerthreadreturnedwithbadiopriority"></a>バグ チェック 0x128:ワーカー\_スレッド\_から返された\_WITH\_不良\_IO\_優先順位


ワーカー\_スレッド\_から返された\_WITH\_不良\_IO\_優先度のバグ チェックが 0x00000128 の値を持ちます。 これは、ワーカー スレッド IOPriority が呼び出されるワーカー ルーチンによって誤って変更されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="workerthreadreturnedwithbadiopriority-parameters"></a>ワーカー\_スレッド\_から返された\_WITH\_不良\_IO\_優先度パラメーター


| パラメーター | 説明                                                                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1         | ワーカーのルーチンのアドレス (使用して、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)コマンド問題のあるドライバーを検索するには、このアドレスを) |
| 2         | 現在の IoPrioirity 値                                                                                                                               |
| 3         | 作業項目のパラメーター                                                                                                                                      |
| 4         | 作業項目のアドレス                                                                                                                                        |

 

 

 




