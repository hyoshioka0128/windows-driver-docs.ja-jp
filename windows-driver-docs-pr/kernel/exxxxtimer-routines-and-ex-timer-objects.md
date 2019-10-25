---
title: Exxxx TIMER ルーチンと EX_TIMER オブジェクト
description: Windows 8.1 以降では、一連の Exxxx タイマールーチンを使用して、タイマーを管理できます。
ms.assetid: 5F2622F5-4D1A-48F4-9FF5-27DEC6109266
keywords:
- タイマー WDK カーネル
- タイマーオブジェクト WDK カーネル
- タイマーオブジェクト WDK カーネル、タイマーオブジェクトについて
- カーネルディスパッチャーオブジェクト WDK、タイマーオブジェクト
- ディスパッチャーオブジェクト WDK カーネル、タイマーオブジェクト
- 高解像度タイマー WDK カーネル
- 非ウェイクアップタイマー WDK カーネル
- EX_TIMER
- Exxxx タイマールーチン
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 040ead56fe15c34137ca19cefb627f94d1cf5b97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838701"
---
# <a name="exxxxtimer-routines-and-ex_timer-objects"></a>Exxxx Timer ルーチンおよび EX\_TIMER オブジェクト


Windows 8.1 以降では、一連の**Ex*Xxx*Timer**ルーチンを使用して、タイマーを管理できます。 これらのルーチンは、 [**EX\_timer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造に基づくタイマーオブジェクトを使用します。 **Ex*xxx*タイマー**ルーチンは、Windows 2000 以降で使用できる**Ke*xxx*タイマー**ルーチンの代替です。 Windows 8.1 以降のバージョンの Windows でのみ実行するように意図されたドライバーは、 **Ke*xxx*タイマー**ルーチンの代わりに、 **Ex*xxx*タイマー**ルーチンを使用できます。 Windows の Windows 8.1 以降のバージョンでは、 **Ke*Xxx*タイマー**ルーチンが引き続きサポートされます。

**Ex*xxx*タイマー**ルーチンには、 **Ke*xxx*タイマー**ルーチンによって提供されるすべての重要な機能があります。 さらに、 **Ex*xxx*タイマー**ルーチンでは、Ke タイマーの*種類として、2*種類のタイマーを*サポートして*います。これは、 **Ke*xxx*タイマー**ルーチンではサポートされていません。 高解像度のタイマーは、システムクロックの既定の解決によって精度が制限されているタイマーよりも高い精度で、有効期限を指定できるタイマーです。 No wake タイマーは、低電力状態からの不要なウェイクアッププロセッサを回避するタイマーです。 詳細については、次のトピックを参照してください。

[高解像度タイマー](high-resolution-timers.md)
Windows 8.1 以降で[は、次](no-wake-timers.md)の例のような ***Xxx*タイマー**ルーチンを使用できます。

[**Exallocatetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)
[**Excanceltimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer)
[**Exdeletetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer) 。 [**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)または[**kesettimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)ルーチンの代わりに**ExSetTimer**ルーチンを使用できます。 [**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)ルーチンの代わりに、 **excanceltimer**ルーチンを使用できます。

**Exallocatetimer**ルーチンと**exdeletetimer**ルーチンには、対応する direct **Ke*Xxx*タイマー**がありません。 これらの2つのルーチンは、タイマーオブジェクトを割り当て、解放します。 このタイマーオブジェクトは、システムによって割り当てられる[**EX\_timer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体で、メンバーがドライバーに対して非透過的であることを示します。 これに対して、 **Ke*Xxx*タイマー**ルーチンによって使用されるタイマーオブジェクトは、ドライバーによって割り当てられる[**ktimer**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体です。 ドライバーは、 [**Keinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)または[**Keinitializetimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)ルーチンを呼び出して、このオブジェクトを初期化します。 **Exallocatetimer**は、割り当てるタイマーオブジェクトを初期化します。 **Exdeletetimer**の詳細については、「[システム割り当てタイマーオブジェクトの削除](deleting-a-system-allocated-timer-object.md)」を参照してください。

**例\_タイマー**と**ktimer**構造体は、待機可能なオブジェクトです。 ドライバーは、 **ExSetTimer**、 **KeSetTimer**、または**kesettimerex**を呼び出してタイマーを設定した後、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)や[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)などのルーチンを呼び出して、タイマーの有効期限が切れるのを待ちます。 タイマーオブジェクトは、タイマーの有効期限が切れたときに通知されます。 オプションとして、ドライバーによって実装される[*extimercallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_callback)または[*customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)コールバックルーチンへのポインターを指定できます。このルーチンは、タイマーの有効期限が切れた後にオペレーティングシステムが呼び出します。

**Ke*xxx*タイマー**ルーチンには、 **Ex*xxx*タイマー**ルーチンでは提供されない2つの機能がありますが、ほとんどのドライバーではこれらの機能は必要ありません。

まず、 **Ke*Xxx*タイマー**ルーチンによってタイマーオブジェクトとして使用される**ktimer**構造体は、ドライバーによって割り当てられます。 ドライバーは、リソースが制限され、メモリ割り当てが失敗する状況でも、オブジェクトを確実に使用できるように、このオブジェクトを事前に割り当てることができます。 これに対して、タイマーオブジェクトを割り当てるために**Exallocatetimer**を呼び出すと、リソースの制約付き環境でエラーが発生する可能性があります。 ただし、ほとんどのドライバーは、メモリ割り当てが失敗する環境で動作するように設計する必要があります。ほとんどのドライバーは、タイマーオブジェクトを割り当てて初期化する**Exallocatetimer**ルーチンを使用すると便利です。

2つ目は、タイマーオブジェクトがシグナル状態であるかどうかを示す、 [**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)ルーチンに相当する**例*Xxx*タイマー**がないことです。 ただし、このルーチンはほとんど使用されません。 必要に応じて、 **Ex*Xxx*タイマー**ルーチンを使用するドライバーは、ドライバーによって提供される*extimercallback*コールバックルーチンによって設定されたブール値を読み取って、**タイマーオブジェクトがシグナル状態であるかどうかを確認できます。ExAllocateTimer**ルーチン。

 

 




