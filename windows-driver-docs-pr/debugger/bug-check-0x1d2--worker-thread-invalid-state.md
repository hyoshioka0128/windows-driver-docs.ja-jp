---
title: バグ チェック 0x1D2 WORKER_THREAD_INVALID_STATE
description: WORKER_THREAD_INVALID_STATE のバグ チェックでは、0x000001D2 の値を持ちます。
keywords:
- バグ チェック 0x1D2 WORKER_THREAD_INVALID_STATE
- WORKER_THREAD_INVALID_STATE
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WORKER_THREAD_INVALID_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31f1110352657961d029de8934e4d074c435bb8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367571"
---
# <a name="bug-check-bug-check-0x1d2-workerthreadinvalidstate"></a>チェックのバグ チェック 0x1D2 をバグします。ワーカー\_スレッド\_無効な\_状態 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


ワーカー\_スレッド\_無効な\_状態のバグ チェックが 0x000001D2 の値を持ちます。 

このエラーは、実行ワーカー スレッドが無効な状態であることを示します。

## <a name="workerthreadinvalidstate-parameters"></a>ワーカー\_スレッド\_無効な\_状態パラメーター

パラメーター | 説明 
|---------|--------------|
1 | エラーの種類
2 | ワーカー スレッドのアドレス
3 | 予約済み
4 | 予約済み



**パラメーター 1 の値**

  0x0 :終了処理中のワーカー スレッドが未処理の I/O
  
  2 - ワーカー スレッドのアドレス
  
  3-予約されています
  
  4-予約されています
