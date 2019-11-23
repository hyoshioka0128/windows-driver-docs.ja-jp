---
title: I/O キューのディスパッチ モードの構成
description: I/O キューのディスパッチ モードの構成
ms.assetid: 7603c3fd-a4cb-4174-ad14-f57efedfe9de
keywords:
- WDK の同期の UMDF
- キューディスパッチモード WDK UMDF
- ディスパッチモード WDK UMDF
- I/o キュー WDK UMDF
- キュー WDK UMDF
- シーケンシャルディスパッチモード WDK UMDF
- パラレルディスパッチモード WDK UMDF
- 手動ディスパッチモード WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f09c0c4bda351144b1469778101523896b8ba907
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843645"
---
# <a name="configuring-dispatch-mode-for-an-io-queue"></a>I/O キューのディスパッチ モードの構成


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

アプリケーションからの i/o 要求が到着すると、フレームワークは各要求を適切な i/o キューに配置します。 要求がドライバーに配信される方法とタイミングは、ドライバーが i/o キューのディスパッチを構成する方法と、ドライバーが[コールバック関数の同期を指定](specifying-a-callback-synchronization-mode.md)する方法によって異なります。 また、i/o キューは、デバイスが適切な状態になるまで、UMDF の PnP および電源管理サブシステムとやり取りして、i/o 要求をキューに保持します。

I/o キューのディスパッチモードが[同期モード](specifying-a-callback-synchronization-mode.md)に関連していない   に**注意**してください。 I/o キューのディスパッチ構成では、ドライバーが特定の時点で処理を受け入れることができる要求の数を制御します。一方、同期は、要求を表示またはキャンセルするイベントコールバック関数の同時実行を制御します。 ただし、いくつかの操作モードは、[ディスパッチモードと同期モードを組み合わせる](combining-dispatch-and-synchronization-modes.md)ことによって作成されます。

 

ドライバーは、 [**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドを呼び出して既定のキューを構成するか、セカンダリキューを作成するときに、i/o キューのディスパッチを構成します。 ドライバーでは、 [**WDF\_IO\_キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_queue_dispatch_type)の値の1つを指定して、 **Iwdfdevice:: CreateIoQueue**の*DispatchType*パラメーターに\_ディスパッチ\_型の列挙型を指定して、ディスパッチモードを識別できます。 [I/o キューオブジェクト](framework-i-o-queue-object.md)は、次のディスパッチモードをサポートできます。

-   シーケンシャル

    順次ディスパッチモードは、 **WdfIoQueueDispatchSequential**値を使用して指定します。 このディスパッチモードでは、処理状態のキューによってイベントが発生するので、ドライバーは一度に1つの要求のみを処理します。 キューは、ドライバーが現在の要求の処理を終了するか、 [**IWDFIoRequest:: ForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-forwardtoioqueue)メソッドを呼び出して要求をキューへするまで、追加の要求をすべて延期します。 現在の要求が完了するか転送されると、キューは次の要求を提供するためにイベントを発生させます。

-   Parallel

    並列ディスパッチモードは、 **WdfIoQueueDispatchParallel**値を使用して指定します。 このディスパッチモードでは、i/o 要求がドライバーで使用できるようになるとすぐに、処理状態のキューによってイベントが発生します。 ドライバーは、i/o 要求を受信すると、次のいずれかの方法で i/o 要求を処理できます。

    -   ドライバーは、 [**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドのいずれかを呼び出して、i/o 要求を直ちに完了します。 I/o 要求が無効であるか、サービスを提供できない場合、またはデータを格納しているバッファーまたはキャッシュからデータをコピーすることによって完了できる場合、ドライバーは i/o 要求を直ちに完了します。
    -   ドライバーは、 [**IWDFIoRequest:: ForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-forwardtoioqueue)メソッドを呼び出して、i/o 要求をキューへします。
    -   ドライバーは、 [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出して、i/o 要求を下位レベルのドライバーに渡します。
-   Manual

    手動ディスパッチモードは、 **WdfIoQueueDispatchManual**値を使用して指定します。 このディスパッチモードでは、要求がキューに到着すると、i/o キューはドライバーに自動的に通知しません。 ドライバーは、 [**Iwdfioqueue:: RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)メソッドを呼び出して、キューから要求を手動で取得する必要があります。 これはポーリングモデルです。

    UMDF バージョン1.9 以降では、ドライバーが手動ディスパッチモードを使用している場合、 [**IWDFIoRequest2:: キューへ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-requeue)を呼び出して、ドライバーによって取得された i/o キューの先頭に i/o 要求を返すことができます。 **IWDFIoRequest2:: キューへ**を呼び出すと、ドライバーの次の[**Iwdfioqueue:: RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)の呼び出しで、キューの要求が取得されます。

すべてのディスパッチモードでは、ドライバーが要求を処理するか、要求が取り消されるまで、 [i/o キューオブジェクト](framework-i-o-queue-object.md)は要求を受信して追跡します。

ドライバーがシリアルディスパッチまたはパラレルディスパッチのためにキューを構成した場合、ドライバーがキューを作成したとき、または既定のキューを構成したときに、ドライバーによって登録されたコールバック関数を介して、要求をドライバーに通知します。 詳細については、「 [I/o キューイベントコールバック関数](i-o-queue-event-callback-functions.md)」を参照してください。

 

 





