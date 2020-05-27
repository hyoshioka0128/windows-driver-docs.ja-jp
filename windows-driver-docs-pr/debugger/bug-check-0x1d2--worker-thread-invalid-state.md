---
title: バグチェック 0x1D2 WORKER_THREAD_INVALID_STATE
description: WORKER_THREAD_INVALID_STATE バグチェックの値は0x000001D2 です。
keywords:
- バグチェック 0x1D2 WORKER_THREAD_INVALID_STATE
- WORKER_THREAD_INVALID_STATE
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WORKER_THREAD_INVALID_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1075d939b592b53653f07cc29aeaafe3314747d7
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851565"
---
# <a name="bug-check-0x1d2-worker_thread_invalid_state"></a>バグチェック 0x1D2: ワーカー \_ スレッドの \_ 状態が無効です \_ 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


ワーカー \_ スレッドの \_ 無効な \_ 状態のバグチェックには、0x000001d2 という値が指定されています。 

このエラーは、executive ワーカースレッドの状態が無効であることを示します。

## <a name="worker_thread_invalid_state-parameters"></a>ワーカー \_ スレッド \_ の \_ 状態パラメーターが無効です

パラメーター | 説明 
|---------|--------------|
1 | エラーの種類
2 | ワーカースレッドのアドレス
3 | 予約済み
4 | 予約済み



**パラメーター1の値**

  0x0: 終了処理中のワーカースレッドに未処理の i/o がある
  
  2-ワーカースレッドのアドレス
  
  3-予約済み
  
  4-予約済み
