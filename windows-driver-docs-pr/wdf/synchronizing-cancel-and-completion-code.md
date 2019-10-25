---
title: キャンセルと完了コードの同期
description: キャンセルと完了コードの同期
ms.assetid: 4c302fc5-cb14-46e5-80c8-8dbf62486905
keywords:
- WDK KMDF の要求の処理、要求の取り消し
- I/o 要求 WDK KMDF、取り消し
- WDK KMDF の同期
- i/o 要求の完了 (WDK KMDF)
- 要求の処理 WDK KMDF、同期
- I/o 要求 WDK KMDF、同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e37cf0ea5e71db85410bc0c594a749f5d4b132
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831661"
---
# <a name="synchronizing-cancel-and-completion-code"></a>キャンセルと完了コードの同期





ドライバーが[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出して i/o 要求をキャンセルできる場合、同期の問題が発生する可能性があります。 たとえば、ドライバーとデバイスは、 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)と[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)のコールバック関数によってデバイスの i/o 操作を非同期に実行し、 *EvtInterruptDpc*と[*evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)の両方のコールバックを実行することがあります。関数には、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)の呼び出しを含めることができます。

ドライバーは、要求を完了またはキャンセルするために、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を1回だけ呼び出す必要があります。 ただし、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数と[*evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)関数が相互に同期されていない場合、フレームワークは、もう一方のを実行している間に1つを呼び出すことができます。

自動同期によってコールバック関数が一度に1つずつ呼び出されるため、ドライバーでフレームワークの[自動同期](using-automatic-synchronization.md)を使用すると、この問題を簡単に回避できます。

ドライバーがフレームワークの自動同期を使用しない場合は、[フレームワークロック](using-framework-locks.md)を使用してキャンセルと完了コードを同期できます。

ドライバーがフレームワークの自動同期を使用するか、独自の同期を提供するかにかかわらず、ドライバーの[*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数は[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出して要求をキャンセルする必要があります。 ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、次のように[**Wdfrequestunmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)を呼び出す必要があります。

```cpp
Status = WdfRequestUnmarkCancelable(Request);
if( Status != STATUS_CANCELLED ) {
    WdfRequestComplete(Request, RequestStatus);
    }
```

このコードにより、ドライバーが要求をキャンセルするために既に呼び出されている場合、その要求を完了するために、ドライバーが[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出さないようにします。

ドライバーが**wdfrequestunmarkmarkを**呼び出すときに従う必要がある規則の詳細については、「 [**wdfrequestunmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)可能」を参照してください。

 

 





