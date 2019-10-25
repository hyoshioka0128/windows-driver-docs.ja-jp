---
title: 送信済み要求のキャンセルの同期
description: 送信済み要求のキャンセルの同期
ms.assetid: e7ec65c9-bc7b-46ea-853d-3e23b1763666
keywords:
- WDK KMDF の要求の処理、要求の取り消し
- I/o 要求 WDK KMDF、取り消し
- WDK KMDF の同期
- 要求の処理 WDK KMDF、同期
- I/o 要求 WDK KMDF、同期
- 要求のキャンセルの送信 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0afc782b653fcf0d5b9c6fbb01e5fdda34a01d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831650"
---
# <a name="synchronizing-cancellation-of-sent-requests"></a>送信済み要求のキャンセルの同期


ドライバーは、i/o ターゲットに転送された i/o 要求をキャンセルしようとするときに、有効な要求ハンドルを[**Wdfrequestcancelの要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)メソッドに渡す必要があります。 I/o ターゲットが要求を完了すると、要求ハンドルは無効になります。これは、ドライバーの完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数が[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) (要求オブジェクトを削除しようとする) を呼び出すためです。

この問題を回避するために、ドライバーは、要求オブジェクトの[コレクション](framework-object-collections.md)を作成するなどして、i/o ターゲットに送信された要求を追跡することができます。 ドライバーは[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))を呼び出して、コレクションへのアクセスを同期できます。

ドライバーの完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数が呼び出されると、ロックを取得し、完了した要求のハンドルをコレクションから削除し、 [**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))を呼び出してロックを解放します。

ドライバーが i/o ターゲットに転送した要求をキャンセルしようとする前に、ドライバーは次のことを実行できます。

1.  [**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))を呼び出して、スピンロックを取得します。

2.  コレクション内で要求オブジェクトのハンドルを検索し、ドライバーの完了ルーチンが要求を完了していないこと、およびコレクションからハンドルを削除していないことを確認します。

3.  オブジェクトを削除できないように、 [**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)を呼び出して要求オブジェクトの参照カウントをインクリメントします。

4.  [**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))を呼び出して、スピンロックを解除します。

5.  [**Wdfrequestcancelの要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)を呼び出します。

6.  [**Wdfobjectdereference 参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)を呼び出して、オブジェクトの参照カウントをデクリメントします。

このシーケンスにより、ドライバーの完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)であっても、ドライバーが[**Wdfrequestcancelの要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)を呼び出す前に、要求のハンドルが有効であることが保証されます。コールバック関数が[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出しました。

 

 





