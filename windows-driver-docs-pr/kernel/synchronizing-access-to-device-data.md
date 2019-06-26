---
title: デバイス データへのアクセスの同期
description: デバイス データへのアクセスの同期
ms.assetid: aaed8006-6773-4d20-b3a0-b48131f728c6
keywords:
- 割り込みサービス ルーチン WDK カーネルの同期
- Isr WDK カーネルでは、同期
- オブジェクトの WDK カーネル、同期を中断します。
- 同期の WDK カーネル、割り込み
- 1 つの割り込みのベクトルの WDK カーネル
- クリティカル セクション ルーチン WDK カーネル
- 割り込みスピン ロック WDK カーネル
- スピン ロック WDK カーネル
- 同期の WDK カーネル、デバイスのデータへのアクセスします。
- SynchCritSection
- SynchronizeIrql
- SpinLock パラメーター
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50bc4866e79f5b08720ceb7d664cd51580b0fd91
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355491"
---
# <a name="synchronizing-access-to-device-data"></a>デバイス データへのアクセスの同期





通常、ドライバーの[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)または[ *InterruptMessageService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)ルーチン (Isr) は、ドライバーのデータへのアクセスを共有する必要があり、その他のドライバーのルーチンのハードウェア リソース。 各ルーチンは、これへの排他アクセスで一時的に保証されるので、共有データとリソースにアクセスを同期する重要なは Isr は、管理者特権での IRQL で割り込みコンテキストで実行されるため、システムは、複数のプロセッサを必要がありますので、中断することがなく共有情報。

システム内で ISR を実行することによってこの同期をサポートする、*クリティカル セクションの割り込み*します。 割り込みが割り当てられたスピンロック、*スピン ロックを中断*、IRQL、および、 *IRQL の同期を中断*します。 システムでは、IRQL の割り込みの同期に、プロセッサの IRQL を発生させるコードを実行する前に、割り込みスピン ロックを取得して共有の情報へのクリティカル セクションの排他アクセスで実行されるこのコードを保証します。 システムは常にその ISR. を実行する前に、割り込みのクリティカル セクションに移行します。 異なる割り込みは、割り込みスピン ロックおよび同期 IRQL を共有して、同じクリティカル セクションを共有できます。

ドライバーが指定することによって、割り込みのクリティカル セクションで実行されるコードを実装する[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチン。 ドライバーを使用する場合[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出す、 *SynchCritSection* 、日常的なシステムが自動的に入力、クリティカル セクションの割り込み指定された、 *Interrupt*パラメーター。

割り込みの同期の IRQL が中断されてから、現在のプロセッサを防止するプロセッサの IRQL を発生させるより高い同期 IRQL で割り込みによってを除きます。 スピン ロックを取得すると、他のプロセッサはそのスピン ロックに関連付けられている、クリティカル セクションのコードを実行できなくなります。

ドライバーを呼び出すと、システム割り当てます割り込みスピン ロックおよび同期 IRQL 割り込みの[ **IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)します。 ほとんどの場合、ドライバーが両方の値を決定するシステムを許可することができます。

-   ドライバーの接続を使用している場合\_行\_ベースまたは CONNECT\_メッセージ\_ベースのバージョンの**IoConnectInterruptEx**を指定し、 **NULL**スピン ロックでは、すべてのデバイスの割り込みの間で共有する、スピン ロックに割り当てられます。 システムでは、同期 IRQL の値も決定します (ドライバーは高い値を指定必要に応じて)。 すべてのドライバーの割り込みにより、同じクリティカル セクションが共有されます。

-   ドライバーの接続を使用している場合\_完全\_の指定されたバージョン**IoConnectInterruptEx**であり、1 つの割り込みベクトルのみ、ドライバーを指定できます、 **NULL**スピン ロックします。 のみその特定の割り込み、独自の重要なセクションが表示されます、スピン ロックに割り当てられます。

接続を使用する場合にのみ、ドライバーはスピン ロックを割り当てる必要があります\_完全\_の指定されたバージョン**IoConnectInterruptEx**と同じ重大を共有する複数の割り込みベクターがある場合セクション。 ドライバーを使用して、独自のスピン ロックおよび同期 IRQL を指定できます、**スピンロック**と**SynchronizeIrql**のメンバー **IO\_CONNECT\_割り込み\_パラメーター**します。 詳細については、次を参照してください。 [ **IO\_CONNECT\_INTERRUPT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_connect_interrupt_parameters)します。

書き込みとクリティカル セクションの入力については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

 

 




