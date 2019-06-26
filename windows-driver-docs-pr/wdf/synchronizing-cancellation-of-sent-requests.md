---
title: 送信済み要求のキャンセルの同期
description: 送信済み要求のキャンセルの同期
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
ms.openlocfilehash: 45c64cc59bb9af5e3095d958076bdb7b5a3d9558
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369497"
---
# <a name="synchronizing-cancellation-of-sent-requests"></a>送信済み要求のキャンセルの同期


ドライバーが有効な要求を識別するハンドルを渡すことを確認する必要があります、ドライバーが、I/O のターゲットに転送する I/O 要求をキャンセルしようとしたとき、 [ **WdfRequestCancelSentRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)メソッド。 要求ハンドルが I/O ターゲットには、要求が完了すると無効になるドライバーの[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数が呼び出す[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete) (これは要求オブジェクトを削除する試行)。

この問題を回避するドライバーの追跡できることがターゲットに送信 I/O でなどを作成する要求を[コレクション](framework-object-collections.md)の要求オブジェクト。 ドライバーが呼び出せる[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))コレクションへのアクセスを同期します。

ときに、ドライバーの[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数が呼び出されると、ロックを獲得コレクション、および呼び出しから完了した要求のハンドルを削除します[  **。WdfSpinLockRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))ロックを解除します。

ドライバーが I/O のターゲットに転送要求をキャンセルする前に、ドライバーでは次のことができます。

1.  呼び出す[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))スピン ロックを取得します。

2.  ドライバーの完了のルーチンが要求を完了し、ハンドルをコレクションから削除していないことを確認する、コレクション内の要求オブジェクトのハンドルを検索します。

3.  呼び出す[ **WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)オブジェクトを削除できないように、要求をインクリメントするオブジェクトの参照をカウントします。

4.  呼び出す[ **WdfSpinLockRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))スピン ロックを解除します。

5.  呼び出す[ **WdfRequestCancelSentRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)します。

6.  呼び出す[ **WdfObjectDereference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)オブジェクトの参照カウントをデクリメントします。

I/O ターゲット ドライバー呼び出しの前に、要求が完了するとこのシーケンスにより[ **WdfRequestCancelSentRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)、(インクリメントされた参照のため、要求のハンドルがまだ有効数) の場合でも、ドライバーの[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数の呼び出し[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

 

 





