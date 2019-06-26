---
title: ExXxxTimer ルーチンと EX_TIMER オブジェクト
description: Windows 8.1 以降、ExXxxTimer ルーチンの包括的なセットはタイマーの管理に使用できます。
ms.assetid: 5F2622F5-4D1A-48F4-9FF5-27DEC6109266
keywords:
- タイマーの WDK カーネル
- タイマー オブジェクトの WDK カーネル
- タイマー オブジェクトについて、タイマー オブジェクトの WDK カーネル
- カーネルのディスパッチャー オブジェクト WDK、タイマー オブジェクト
- ディスパッチャー オブジェクト WDK カーネル、タイマー オブジェクト
- 高分解能タイマー WDK カーネル
- no ウェイク アップ タイマー WDK カーネル
- EX_TIMER
- ExXxxTimer ルーチン
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d2d669547bb7559dad9d1cf69c5c8ecfcc63b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386617"
---
# <a name="exxxxtimer-routines-and-extimer-objects"></a>ExXxxTimer ルーチンと EX\_タイマー オブジェクト


包括的な設定を Windows 8.1 以降、 **Ex*Xxx*タイマー**ルーチンがタイマーの管理に使用します。 これらのルーチンを使用して、タイマー オブジェクトに基づく、 [ **EX\_タイマー** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体。 **Ex*Xxx*タイマー**ルーチンは、置換、 **Ke*Xxx*タイマー**ルーチンで、Windows 2000 以降を利用します。 ドライバーは Windows 8.1 でのみ実行するものし、以降のバージョンの Windows を使用できます、 **Ex*Xxx*タイマー**ルーチンの代わりに、 **Ke*Xxx*タイマー**ルーチン。 Windows 8.1 と Windows の以降のバージョンがサポートするために引き続き、 **Ke*Xxx*タイマー**ルーチン。

**Ex*Xxx*タイマー**ルーチンによって提供されるすべての重要な機能がある、 **Ke*Xxx*タイマー**ルーチン。 さらに、 **Ex*Xxx*タイマー**ルーチン タイマーの 2 つの型をサポートする*高分解能タイマー*と*いいえウェイク タイマー*ではないです。サポートされている、 **Ke*Xxx*タイマー**ルーチン。 高解像度のタイマーは、タイマーのタイマーの精度は、システム クロックの既定の解像度によって制限されます。 より高い精度での有効期限を指定できます。 No ウェイク アップ タイマーは、低電力状態からのプロセッサを不必要にウェイク アップを回避するタイマーです。 詳しくは、次のトピックをご覧ください。

[高分解能タイマー](high-resolution-timers.md)
[いいえウェイク アップ タイマー](no-wake-timers.md) Windows 8.1、次で始まる**Ex*Xxx*タイマー**使用できるルーチンは。

[**ExAllocateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)
[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)
[**ExCancelTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excanceltimer) 
 [ **ExDeleteTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletetimer) 、 **ExSetTimer**ルーチンは、の代わりに使用できる、 [ **KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)または[ **KeSetTimerEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)ルーチン。 **ExCancelTimer**ルーチンは、の代わりに使用できる、 [ **KeCancelTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kecanceltimer)ルーチン。

**ExAllocateTimer**と**ExDeleteTimer**ルーチンに直接あるありません**Ke*Xxx*タイマー**の対応します。 これら 2 つのルーチンを割り当て、タイマー オブジェクトを解放します。 このタイマー オブジェクトは、システムによって割り当てられた[ **EX\_タイマー** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)のメンバーは、ドライバーを非透過構造体。 タイマー オブジェクトを使用する一方、 **Ke*Xxx*タイマー**ルーチンは、ドライバーによって割り当てられた[ **KTIMER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体。 ドライバーの呼び出し、 [ **KeInitializeTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimer)または[ **KeInitializeTimerEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializetimerex)ルーチンをこのオブジェクトを初期化します。 **ExAllocateTimer**を割り当てたタイマー オブジェクトを初期化します。 詳細については**ExDeleteTimer**を参照してください[System-Allocated タイマー オブジェクトを削除する](deleting-a-system-allocated-timer-object.md)します。

**EX\_タイマー**と**KTIMER**の構造は待機可能オブジェクト。 ドライバーを呼び出してから**ExSetTimer**、 **KeSetTimer**、または**KeSetTimerEx**タイマーを設定するドライバーを呼び出せるルーチンなど[ **Kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)または[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)タイマーが切れるを待機します。 タイマー オブジェクトは、タイマーの期限が切れたときに通知されます。 オプションとして、ドライバーがドライバー実装へのポインターを提供できる[ *ExTimerCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ext_callback)または[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)コールバック ルーチンオペレーティング システムが、タイマーの期限が切れた後を呼び出します。

**Ke*Xxx*タイマー**ルーチンで提供されていない 2 つの機能がある、 **Ex*Xxx*タイマー**ルーチンが、これらの機能ほとんどのドライバーでは必要ありません。

まず、 **KTIMER**によってタイマー オブジェクトとして使用される構造体、 **Ke*Xxx*タイマー**ルーチンは、ドライバーによって割り当てられました。 ドライバーは、オブジェクトがリソースを制限し、メモリ割り当てが失敗する状況であっても使用できることを確認するには、このオブジェクトを事前に割り当てることができます。 呼び出しとは異なり、 **ExAllocateTimer**タイマーを割り当てるリソースが限られた環境でオブジェクトが失敗します。 ただし、いくつかのドライバーは、どのメモリ割り当ての失敗での環境で動作するように設計する必要があります、ほとんどのドライバーの利便性のメリット、 **ExAllocateTimer**ルーチンを割り当てるし、タイマー オブジェクトを初期化します。

第二に、ありません**Ex*Xxx*タイマー**と同等の[ **KeReadStateTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereadstatetimer)ルーチンで、タイマー オブジェクトがであるかどうかを示しますシグナルの状態。 ただし、このルーチンはほとんど使用されません。 必要に応じて、ドライバーを使用する場合は、 **Ex*Xxx*タイマー**ルーチンがによって設定されるブール値を読み取ることで、タイマー オブジェクトがシグナル状態でがかどうかを確認することができます、 *ExTimerCallback*にドライバーを提供するコールバック ルーチン、 **ExAllocateTimer**ルーチン。

 

 




