---
title: ISR をアクティブまたは非アクティブにする
description: Windows 8 以降では、ドライバーは IoReportInterruptActive または IoReportInterruptInactive ルーチンを呼び出して、登録されている割り込みサービスルーチン (ISR) をアクティブまたは非アクティブにすることができます。
ms.assetid: 788D9341-D1F8-4126-8C30-AA49DE27F4BB
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 98df2d6f2396a33cb175eb0d5b2ec89ecfc6ef33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838551"
---
# <a name="making-an-isr-active-or-inactive"></a>ISR をアクティブまたは非アクティブにする


Windows 8 以降では、ドライバーは[**IoReportInterruptActive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreportinterruptactive)または[**IoReportInterruptInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreportinterruptinactive)ルーチンを呼び出して、登録されている割り込みサービスルーチン (ISR) をアクティブまたは非アクティブにすることができます。

ISR を登録し、ISR を割り込みまたは割り込みのセットに接続するために、ドライバーは[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチンを呼び出します。 ISR が登録されると、ドライバーは**IoReportInterruptActive**と**IoReportInterruptInactive**を使用して、isr の登録を変更せずに、軽量 (または "ソフト") の接続および切断操作を実行できます。 **IoReportInterruptInactive**は、関連付けられている割り込みまたは割り込みをソフト切断することによって、ISR への呼び出しを無効にします。 **IoReportInterruptActive** soft-これらの割り込みを接続して、ISR の呼び出しを有効にします。

たとえば、ドライバーが**IoReportInterruptInactive**を呼び出して、デバイスが d0 の電源状態を終了する前に割り込みのセットを論理的に切断し、 **IoReportInterruptActive**を呼び出して、デバイスが d0 に入った後にこれらの割り込みをソフト接続する場合があります。 原則として、ドライバーは、デバイスが D0 を終了する前に[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)を呼び出し、デバイスが d0 に入った後に**IoConnectInterruptEx**を呼び出すことができます。 ただし、 **IoReportInterrupt * Xxx*** の呼び出しは、 **IoConnectInterruptEx**と**IoDisconnectInterruptEx**の呼び出しよりも高速です。 **IoConnectInterruptEx**と**IoDisconnectInterruptEx**の呼び出しは、さまざまな理由で失敗する可能性があります (たとえば、システムリソースが不足している場合)、 **IoReportInterrupt * Xxx*** 呼び出しはめったに発生しません。 また、 **IoReportInterrupt * Xxx*** ルーチンは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。一方、 **IoConnectInterruptEx**と**IODISCONNECTINTERRUPTEX**はパッシブな\_レベルでのみ呼び出すことができます。

既定では、 **IoConnectInterruptEx**が isr を正常に登録した後、isr がアクティブ (および isr の呼び出しが有効) になります。

**IoReportInterruptInactive**と**IoReportInterruptActive**の呼び出しは省略可能です。 ドライバーがこれらのルーチンを呼び出すことがない場合、登録された ISR は、ドライバーが[**IoDisconnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex)ルーチンを呼び出して ISR の登録を解除するまでアクティブのままになります。

ドライバーは、これらの割り込みの ISR がアクティブになっている場合にのみ、割り込みを発行するようにデバイスを構成する必要があります。 ISR が非アクティブのときにデバイスが割り込みを発行しないようにすると、システムが不安定になる可能性があります。 たとえば、デバイスがレベルでトリガーされた割り込み回線を他のデバイスと共有していて、ISR が非アクティブなときにデバイスが割り込み要求を発行した場合、回線上の他のデバイスの Isr は割り込みを認識できず、割り込みは続行されます. **IoReportInterruptInactive**を呼び出す前に、ドライバーは、割り込みの発行を停止するようにデバイスを構成する必要があります。 **IoReportInterruptActive**を呼び出した後、ドライバーは、割り込みの発行を開始するようにデバイスを構成する必要があります。

ISR の登録を解除すると、現在、ISR がアクティブか非アクティブかに関係なく、ドライバーは**IoDisconnectInterruptEx**を呼び出すことができます。

ISR が既にアクティブになっている場合に発生する**IoReportInterruptActive**呼び出しは無効ですが、エラーとして扱われません。 同様に、ISR が既に非アクティブになっている場合に発生する**IoReportInterruptInactive**呼び出しは無効ですが、エラーとして扱われません。

 

 




