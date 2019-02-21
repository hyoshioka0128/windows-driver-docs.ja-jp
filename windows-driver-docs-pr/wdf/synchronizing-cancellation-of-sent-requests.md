---
title: 同期送信済み要求の取り消し
description: 同期送信済み要求の取り消し
ms.assetid: e7ec65c9-bc7b-46ea-853d-3e23b1763666
keywords:
- 要求の WDK KMDF、キャンセル要求を処理します。
- I/O 要求のキャンセルの WDK KMDF
- WDK KMDF の同期
- WDK KMDF、同期処理を要求します。
- I/O は、WDK KMDF、同期を要求します。
- 要求がキャンセルされました WDK KMDF の送信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39880b129b9f812fb276c6d19ec4404f6e40e8be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558576"
---
# <a name="synchronizing-cancellation-of-sent-requests"></a>同期送信済み要求の取り消し


ドライバーが有効な要求を識別するハンドルを渡すことを確認する必要があります、ドライバーが、I/O のターゲットに転送する I/O 要求をキャンセルしようとしたとき、 [ **WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941)メソッド。 要求ハンドルが I/O ターゲットには、要求が完了すると無効になるドライバーの[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数が呼び出す[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) (これは要求オブジェクトを削除する試行)。

この問題を回避するドライバーの追跡できることがターゲットに送信 I/O でなどを作成する要求を[コレクション](framework-object-collections.md)の要求オブジェクト。 ドライバーが呼び出せる[ **WdfSpinLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff550040)コレクションへのアクセスを同期します。

ときに、ドライバーの[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数が呼び出されると、ロックを獲得コレクション、および呼び出しから完了した要求のハンドルを削除します[  **。WdfSpinLockRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff550044)ロックを解除します。

ドライバーが I/O のターゲットに転送要求をキャンセルする前に、ドライバーでは次のことができます。

1.  呼び出す[ **WdfSpinLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff550040)スピン ロックを取得します。

2.  ドライバーの完了のルーチンが要求を完了し、ハンドルをコレクションから削除していないことを確認する、コレクション内の要求オブジェクトのハンドルを検索します。

3.  呼び出す[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)オブジェクトを削除できないように、要求をインクリメントするオブジェクトの参照をカウントします。

4.  呼び出す[ **WdfSpinLockRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff550044)スピン ロックを解除します。

5.  呼び出す[ **WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)します。

6.  呼び出す[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)オブジェクトの参照カウントをデクリメントします。

I/O ターゲット ドライバー呼び出しの前に、要求が完了するとこのシーケンスにより[ **WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)、(インクリメントされた参照のため、要求のハンドルがまだ有効数) の場合でも、ドライバーの[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数の呼び出し[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)します。

 

 





