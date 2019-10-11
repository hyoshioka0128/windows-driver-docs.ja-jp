---
title: デバイス データへのアクセスの同期
description: デバイス データへのアクセスの同期
ms.assetid: aaed8006-6773-4d20-b3a0-b48131f728c6
keywords:
- 割り込みサービスルーチン WDK カーネル、同期
- Isr WDK カーネル、同期
- 割り込みオブジェクト WDK カーネル、同期
- 同期 WDK カーネル、割り込み
- シングル割り込みベクター WDK カーネル
- クリティカルセクションルーチン WDK カーネル
- 割り込みスピンロックの WDK カーネル
- スピンロック WDK カーネル
- 同期 WDK カーネル、デバイスデータアクセス
- SynchCritSection
- SynchronizeIrql
- スピンロックパラメーター
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 500a77927113793733bdef46f947ffb5bb3f1d6a
ms.sourcegitcommit: 8fdbd7d16dd2393e5df0a87388aed91d2898cd71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2019
ms.locfileid: "72165027"
---
# <a name="synchronizing-access-to-device-data"></a>デバイス データへのアクセスの同期





通常、ドライバーの[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)ルーチンまたは[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)ルーチン (isr) は、ドライバーデータとハードウェアリソースへのアクセスを他のドライバールーチンと共有する必要があります。 Isr は、昇格された IRQL で割り込みコンテキストで実行されるため、システムには複数のプロセッサが存在する可能性があるため、共有データとリソースへのアクセスを同期することが重要です。これにより、各ルーチンが一時的にこの共有情報 (中断なし)。

システムは、*割り込みクリティカルセクション*内で ISR を実行することで、この同期をサポートします。 割り込みには、スピンロック、*割り込みスピンロック*、および irql (*割り込み同期 irql*) が割り当てられています。 システムは、プロセッサの IRQL を割り込み同期 IRQL にし、コードを実行する前に割り込みスピンロックを取得することで、クリティカルセクション内でこのコードが実行されることを保証します。 システムは、ISR を実行する前に、常に割り込みのクリティカルセクションを入力します。 割り込みスピンロックと同期 IRQL を共有することで、異なる割り込みで同じクリティカルセクションを共有できます。

ドライバーは、 [*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンを指定することによって、割り込みの重要なセクションで実行されるコードを実装できます。 ドライバーが[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を使用して*SynchCritSection*ルーチンを呼び出すと、*割り込み*パラメーターによって指定された割り込みのクリティカルセクションが自動的に入力されます。

プロセッサの IRQL を割り込みの同期 IRQL に上げると、現在のプロセッサが中断されるのを防ぐことができます。ただし、同期 IRQL が高い割り込みは除きます。 スピンロックを取得すると、そのスピンロックに関連付けられた重要なセクションコードが他のプロセッサによって実行されるのを防ぐことができます。

ドライバーが[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)を呼び出すと、割り込みに対する割り込みスピンロックと同期 IRQL が割り当てられます。 ほとんどの場合、ドライバーは、システムが両方の値を決定できるようにします。

-   ドライバーが CONNECT @ no__t-0LINE @ no__t-1BASED バージョンの**IoConnectInterruptEx**を使用し、 **NULL**のスピンロックを指定している場合は、割り込み線にスピンロックが割り当てられます。 また、同期 IRQL の値も決定されます (ドライバーでは、必要に応じてより高い値を指定できます)。

-   ドライバーで CONNECT @ no__t-0MESSAGE @ no__t-1BASED バージョンの**IoConnectInterruptEx**を使用し、 **NULL**のスピンロックを指定すると、割り込みメッセージごとにスピンロックが割り当てられます。 また、各メッセージの同期 IRQL の値も決定されます (ドライバーでは、すべてのメッセージに共通する、より高い値を指定できます)。


ドライバーが独自のスピンロックを割り当てる必要があるのは、CONNECT @ no__t-0FULLY @ no__t-1SPECIFIED バージョンの**IoConnectInterruptEx**を使用している場合と、同じクリティカルセクションを共有する必要がある複数の割り込みベクターがある場合のみです。 ドライバーは、 **i/o @ no__t-3CONNECT @ no__t-4INTERRUPT @ NO__T パラメーター**の**スピン**ロックおよび**SynchronizeIrql**メンバーを使用して、独自のスピンロックおよび同期 IRQL を指定できます。 詳細については、「 [**IO @ no__t-2CONNECT @ no__t-3INTERRUPT @ no__t-4PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_connect_interrupt_parameters)」を参照してください。

クリティカルセクションの記述と入力の詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

 

 




