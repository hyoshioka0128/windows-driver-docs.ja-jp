---
title: システムによって割り当てられたタイマー オブジェクトの削除
description: Windows 8.1 以降、ExDeleteTimer ルーチンは、ExAllocateTimer ルーチンによって作成されたタイマーオブジェクトを削除します。
ms.assetid: 7D119448-3890-4E8F-BC79-7FEB3213B693
keywords:
- Exxxx タイマールーチン
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
- ExTimerDeleteCallback
- EX_TIMER
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7938d1e9568e0636b34e0d0e162a8f21a3401cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828393"
---
# <a name="deleting-a-system-allocated-timer-object"></a>システムによって割り当てられたタイマー オブジェクトの削除


Windows 8.1 以降、 [**Exdeletetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer)ルーチンは、 [**exallocatetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)ルーチンによって作成されたタイマーオブジェクトを削除します。 このタイマーオブジェクトは、システムによって割り当てられる[**EX\_timer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体で、メンバーがドライバーに対して非透過的であることを示します。 タイマーオブジェクトが削除される前に、 **Exdeletetimer**は、オブジェクトに対するその他のタイマー操作を無効にし、進行中のオブジェクトに対する保留中の操作をキャンセルまたは完了します。

ドライバーが**Exdeletetimer**を呼び出した後、このルーチンはタイマーオブジェクトを安全に削除できるように、いくつかの手順を実行します。 まず、 **Exdeletetimer**はタイマーオブジェクトを無効としてマークし、そのオブジェクトを使用する新しいタイマー操作がドライバーによって開始されないようにします。 タイマーオブジェクトが無効になると、 [**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)または[**excanceltimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer)ルーチンを呼び出すとすぐに**FALSE**が返され、操作は実行されません。 また、 **Exdeletetimer**への2回目の呼び出しでは**FALSE**が返され、操作は実行されません。

次に、 **exdeletetimer**は、前の**exdeletetimer**への呼び出しからタイマーが保留中かどうかを確認します。 タイマーオブジェクトを無効にしても、オブジェクトが無効になる前に設定されたタイマーはキャンセルされません。 次の2つのいずれかの場合、タイマーオブジェクトが無効になると、以前に設定されたタイマーの有効期限が切れる可能性があります。

-   タイマーは定期的です。
-   タイマーがワンショット (または非周期) であり、まだ期限切れになっていません。

タイマーオブジェクトを無効にした後、定期的なタイマーの有効期限が2回以上になることはありません。

ドライバーが[*Extimercallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_callback)コールバックルーチンを実装している場合、このルーチンの*タイマー*パラメーターは、タイマーの有効期限が切れた場合でも、タイマーオブジェクト (**例\_タイマー**構造) への有効なポインターであることが保証されます。タイマーオブジェクトが無効になっています。

タイマーが保留されていない場合、 **Exdeletetimer**はタイマーオブジェクトを削除し、待機せずに制御を戻します。

**Exdeletetimer**が呼び出されたときにタイマーが保留になっている場合は、ドライバーがこのルーチンに提供する*Cancel*および*Wait*パラメーターの値によって、ルーチンの動作が制御されます。 *Cancel*パラメーターは、保留中のタイマーをキャンセルするかどうかを**exdeletetimer**に指示します。 *Wait*パラメーターは、**タイマーオブジェクト**が削除されるまで待機するかどうかを指定します。

*Cancel*が**false** (この場合、 *Wait*は**false**である必要があります) で、タイマーが保留中の場合、 **exdeletetimer**はタイマーオブジェクトが削除される前にタイマーの有効期限が切れるようにします。 この場合、 **Exdeletetimer**は、タイマーオブジェクトをマークして、保留タイマーの有効期限が切れた後に削除されることを示します (また、 *exdeletetimer*ルーチンへの最後のコールバックが終了します)。 その後、 **Exdeletetimer**は、タイマーが期限切れになるか、オブジェクトが削除されるのを待たずに戻ります。

*Cancel*が**TRUE**の場合、 **exdeletetimer**は、有効期限が切れる前に保留中のタイマーをキャンセルしようとします。 **Exdeletetimer**は、タイマーが正常にキャンセルされた場合に**TRUE**を返します。 **Exdeletetimer**は、タイマーをキャンセルできない場合は**FALSE**を返します。これは、既に有効期限が切れているか、または有効期限が切れているワンショットタイマーの場合です。 Exdeletetimer は、 **exdeletetimer**呼び出しの前に (ワンショットまたは周期的な) タイマーが取り消された場合、またはタイマーが設定されていない場合**にも** **FALSE**を返します。

*Cancel*が**TRUE**で*Wait*が**FALSE**の場合、 **exdeletetimer**は呼び出し元のスレッドをブロックしません。 タイマーオブジェクトを直ちに削除できない場合、 **Exdeletetimer**はタイマーオブジェクトにマークを付けて、保留中のタイマーの期限が切れた後に削除されることを示し、タイマーが期限切れになるか、オブジェクトに対して待機することなく直ちに制御を戻します。削除されます。

*Cancel*と*Wait*の両方が**TRUE**の場合、タイマーオブジェクトを直ちに削除できない場合、 **exdeletetimer**は呼び出し元のスレッドをブロックします。 **Exdeletetimer**は、必要に応じて、タイマーが有効期限切れになり、ドライバーによって実装された*exdeletetimer*ルーチンへのコールバックが終了するまで待機します。 次に、このルーチンがドライバーによって実装されている場合、 **Exdeletetimer**はタイマーオブジェクトを削除し、 [*ExTimerDeleteCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_delete_callback)ルーチンを呼び出します。 最後に、 **Exdeletetimer**はを返します。

ドライバーは、IRQL = ディスパッチ\_レベルで実行されるドライバーの*Exdeletetimer*ルーチンから**exdeletetimer**を呼び出すことができますが、ドライバーはこの呼び出しの*Wait*パラメーターを**FALSE**に設定する必要があります。

オプションとして、ドライバーは、タイマーオブジェクトが削除された後に実行される*ExTimerDeleteCallback*コールバックルーチンを実装できます。 通常、 *ExTimerDeleteCallback*ルーチンは、ドライバーによってタイマーオブジェクトと共に使用するために割り当てられたシステムリソースを解放します。

**Exdeletetimer**は、タイマーオブジェクトが削除された後に実行するドライバーによって実装された*ExTimerDeleteCallback*ルーチンをスケジュールします。このとき、このオブジェクトへのポインターは無効になります。 **Exdeletetimer**呼び出しで*Wait*パラメーターが**TRUE**の場合、 *ExTimerDeleteCallback*ルーチンへのコールバックは、 **exdeletetimer**が戻る前に終了します。 *Wait*が**FALSE**の場合、 *ExTimerDeleteCallback*ルーチンは、 **exdeletetimer**が返される前または後に実行される可能性があります。

詳細については、「 [Ex*Xxx*timer ルーチン」と「Ex\_timer Objects](exxxxtimer-routines-and-ex-timer-objects.md)」を参照してください。

 

 




