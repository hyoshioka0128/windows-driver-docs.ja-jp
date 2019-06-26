---
title: キャンセルと完了コードの同期
description: キャンセルと完了コードの同期
ms.assetid: 4c302fc5-cb14-46e5-80c8-8dbf62486905
keywords:
- 要求の WDK KMDF、キャンセル要求を処理します。
- I/O 要求のキャンセルの WDK KMDF
- WDK KMDF の同期
- WDK KMDF を要求する I/O の完了
- WDK KMDF、同期処理を要求します。
- I/O は、WDK KMDF、同期を要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f41140dc368057be4446ad964e35b5713bd9ee45
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369499"
---
# <a name="synchronizing-cancel-and-completion-code"></a>キャンセルと完了コードの同期





ドライバーを呼び出す場合[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)または[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)する I/O 要求をキャンセル可能ながあります同期の問題の潜在的なです。 など、ドライバーとデバイスの方法では、非同期的にデバイス I/O 操作を実行可能性があります[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)と[ *EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数、および、 *EvtInterruptDpc*と[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数が呼び出しを含む可能性があります[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

ドライバーを呼び出す必要があります[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 1 回だけするか、完了またはキャンセル要求。 しかし、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)と[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数が、相互フレームワークと同期されていません。呼び出すことができますいずれか、その他の実行中にします。

簡単に、ドライバー、フレームワークを使用している場合は、この問題を回避する[自動同期](using-automatic-synchronization.md)自動同期により、コールバック関数が呼び出される 1 つずつためです。

使用できる場合は、ドライバーでは、framework の自動同期を使用しない[framework ロック](using-framework-locks.md)キャンセルおよび終了コードを同期します。

かどうか、ドライバーのフレームワークの自動同期が使用または独自同期化も、ドライバーを提供します[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数を呼び出す必要があります[  **。WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)要求をキャンセルします。 ドライバーの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数を呼び出す必要があります[ **WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)次のようにします。

```cpp
Status = WdfRequestUnmarkCancelable(Request);
if( Status != STATUS_CANCELLED ) {
    WdfRequestComplete(Request, RequestStatus);
    }
```

このコードにより、ドライバーは呼び出しません[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)ドライバーが既に呼び出されている要求をキャンセルする場合は、要求を完了します。

呼び出しには、ドライバーは従う必要があるときにルールの詳細については**WdfRequestUnmarkCancelable**を参照してください[ **WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)します。

 

 





