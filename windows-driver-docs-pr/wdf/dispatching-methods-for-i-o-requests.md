---
title: I/O 要求のディスパッチ方法
description: I/O 要求のディスパッチ方法
ms.assetid: 3e91aa7c-bccf-4eeb-8b68-b1277a690f8c
keywords:
- I/o キュー WDK KMDF、作成
- I/o キュー WDK KMDF、ディスパッチメソッド
- メソッドのディスパッチ (WDK KMDF)
- シーケンシャルディスパッチ WDK KMDF
- WDK KMDF の同期ディスパッチ
- WDK KMDF の並列ディスパッチ
- WDK KMDF の非同期ディスパッチ
- WDK KMDF の手動によるディスパッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be88ba6724347b49864bdc67c0b2f7bc4e30b80c
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242887"
---
# <a name="dispatching-methods-for-io-requests"></a>I/O 要求のディスパッチ方法





ドライバーが[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して i/o キューを作成するときに、キューのディスパッチ方法を指定します。 このフレームワークには、[シーケンシャル](#sequential-dispatching)、[並列](#parallel-dispatching)、[手動](#manual-dispatching)の3つのディスパッチメソッドが用意されています。 ドライバーは、デバイスの[既定の i/o キュー](creating-i-o-queues.md)など、任意の i/o キューに対してこれらのディスパッチ方法を指定できます。

ドライバーは、キューの[**WDF\_io\_queue\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体\_型指定された値を[**ディスパッチ\_、WDF\_io\_キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_queue_dispatch_type)を指定することによって、キューのディスパッチ方法を設定します。

各ディスパッチ方法の使用例については、「 [I/o キューの使用例](example-uses-of-i-o-queues.md)」を参照してください。

### <a href="" id="sequential-dispatching"></a>順次ディスパッチ

ドライバーまたはデバイスで一度にキューからの i/o 要求を1つしか処理できない場合は、*順次ディスパッチ*を使用するようにデバイスの i/o キューを設定する必要があります。これは、*同期ディスパッチ*とも呼ばれます。 この種のディスパッチでは、フレームワークは一度に1つずつドライバーに要求を配信します。 フレームワークは、ドライバーが前回の要求を[完了](completing-i-o-requests.md)、[取り消し](canceling-i-o-requests.md)、または[キュー](requeuing-i-o-requests.md)するまで、次の要求を配信しません。

フレームワークは、ドライバーの[要求ハンドラー](request-handlers.md)のいずれかに要求を配信した後、[要求を処理](processing-i-o-requests.md)します。 ドライバーが要求を[一般的な i/o ターゲット](general-i-o-targets.md)に転送する場合、通常は、i/o ターゲットオブジェクトの同期メソッドの1つを呼び出します。 これらの方法の詳細については、「[同期的に I/o 要求を送信](sending-i-o-requests-synchronously.md)する」を参照してください。 ドライバーは、i/o キューから受信したすべての要求を最終的に[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)する必要があります。

順次ディスパッチ用の i/o キューを設定したドライバーは、 [**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)または[**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)を呼び出して、最後に受信した要求が完了または取り消される前に、別の要求をキューから取得することができます。 これを関数ドライバーで実行すると、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数が以前のハードウェア操作のデータを処理している間に、ドライバーが次のハードウェア操作を開始できるようになります。

複数の i/o キューを作成し、それらを順次ディスパッチ用に設定した場合、フレームワークは各キューから順番に要求をディスパッチしますが、キューは並列で実行されます。 ドライバーまたはデバイスが、任意の種類の一度に1つの要求のみを処理できる場合は、1つの i/o キューで[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数を使用する必要があります。

### <a href="" id="parallel-dispatching"></a>並列ディスパッチ

ドライバーとデバイスが複数の i/o 要求を同時に処理できる場合は、ドライバーが非同期的に要求を処理できるように、*並列ディスパッチ*を使用するようにデバイスの i/o キューを設定できます。 このディスパッチメソッドは、*非同期ディスパッチ*とも呼ばれます。

ドライバーが並列ディスパッチを使用するように i/o キューを設定した場合、フレームワークは、キューで使用できるようになるとすぐに i/o 要求をドライバーに配信します。 その結果、ドライバーは一度に複数の要求を処理しなければならなくなる可能性があります。

ドライバーの[要求ハンドラー](request-handlers.md)の1つが要求を受け取るたびに、ドライバーは[要求を処理](processing-i-o-requests.md)し、要求を[完了](completing-i-o-requests.md)する必要があります。 ドライバーが要求を[一般的な i/o ターゲット](general-i-o-targets.md)に転送する場合は、通常、i/o ターゲットオブジェクトの非同期メソッドを呼び出します。 これらのメソッドの詳細については、「 [I/o 要求を非同期に送信](sending-i-o-requests-asynchronously.md)する」を参照してください。 ドライバーは、i/o キューから受信したすべての要求を最終的に[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)する必要があります。

パラレルディスパッチを使用するドライバーは、 [**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)または[**Wdfioqueuestopを同期的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)に呼び出してキューを一時的に停止した後、 [**wdfioqueuestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)を呼び出してキューを再起動することができます。

### <a href="" id="manual-dispatching"></a>手動によるディスパッチ

ドライバーで i/o 要求の配信を完全に制御できるようにするには、*手動ディスパッチ*を使用するようにデバイスの i/o キューを設定します。これは、ドライバーが明示的に要求しない限り、フレームワークがドライバーに要求を送信しないことを意味します。

手動キューから要求を取得するために、ドライバーは、キューをポーリングするループ内で[**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)または[**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)を呼び出すことができます。 または、ドライバーが[**Wdfioqueuereadynotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuereadynotify)を呼び出して、キューで1つ以上の要求が使用可能になったときにフレームワークが呼び出すコールバック関数を登録できます。 フレームワークがコールバック関数を呼び出すと、ドライバーはループ内で**WdfIoQueueRetrieveNextRequest**または**WdfIoQueueRetrieveRequestByFileObject**を呼び出して要求を取得できます。

ドライバーは、キューから要求を取得した後、[要求を処理](processing-i-o-requests.md)する必要があります。 ドライバーは、最終的に各要求を[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)する必要があります。

 

 





