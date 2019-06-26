---
title: バグ チェック 0x4000008A THREAD_TERMINATE_HELD_MUTEX
description: THREAD_TERMINATE_HELD_MUTEX のバグ チェックでは、0x4000008A の値を持ちます。
ms.assetid: 30A796F0-D622-43F2-8050-C9B62941FBE9
keywords:
- バグ チェック 0x4000008A THREAD_TERMINATE_HELD_MUTEX
- THREAD_TERMINATE_HELD_MUTEX
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THREAD_TERMINATE_HELD_MUTEX
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5645a6182acb58d5211e0ad499998ceeb280f7f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367452"
---
# <a name="bug-check-0x4000008a-threadterminateheldmutex"></a>バグ チェック 0x4000008A:スレッド\_TERMINATE\_保持\_ミュー テックス


スレッド\_TERMINATE\_保持\_ミュー テックスのバグ チェックが 0x4000008A の値を持ちます。 これは、ドライバーが前に、ミュー テックスを解放する可能性がありますが終了したスレッドでミュー テックスを獲得することを示します。 ミュー テックスを解放しないままユーザー モードに戻るドライバーや、ミュー テックスを獲得ドライバーによってこれを発生することができ、スレッドが終了中で実行されている例外をしに原因と発生します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="threadterminateheldmutex-parameters"></a>スレッド\_TERMINATE\_保持\_ミュー テックス パラメーター


| パラメーター | 説明                                      |
|-----------|--------------------------------------------------|
| 1         | KMUTEX を所有している KTHREAD のアドレス。 |
| 2         | 所有されている KMUTEX のアドレス。         |
| 3         | 予約済み                                         |
| 4         | 予約済み                                         |

 

<a name="cause"></a>原因
-----

調査のため、呼び出し履歴を確認します。 システム例外処理ルーチンの後に直接のスタック上のドライバーがあるし、スレッド終了ルーチンでは、このドライバーは、障害ドメインとカーネル ミュー テックスを押しながらハンドルされない例外は発生しないように修正する必要がある場合。 通常のスレッドの終了コード、スタックにのみ表示で、ドライバーは関係ありません実行[ **! プール**](-pool.md)を使用して、または[ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)場合は、it の所有者を見つけることができますを参照してください、ミュー テックス (パラメーター 2) のアドレス。 このバグは、そのミュー テックスの所有者のコードでほぼ確実になります。

 

 




