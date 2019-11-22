---
title: イベント オブジェクトの定義と使用
description: イベント オブジェクトの定義と使用
ms.assetid: 4b7807f0-bbea-4402-b028-9ac73724717f
keywords:
- イベントオブジェクト WDK カーネル
- イベントオブジェクトを待機しています
- 同期イベントの WDK カーネル
- 通知イベントの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186d9fc358ff298d74d54169a44baecee662c9db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828425"
---
# <a name="defining-and-using-an-event-object"></a>イベント オブジェクトの定義と使用





イベントオブジェクトを使用するドライバーは、イベントを待機、設定、クリア、またはリセットする前に[**Keinitializeevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)、 [**IoCreateNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent)、または[**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent)を呼び出す必要があります。 次の図は、スレッドを使用するドライバーが同期にイベントオブジェクトを使用する方法を示しています。

![イベントオブジェクトを待機していることを示す図](images/3evntobj.png)

上の図に示すように、このようなドライバーでは、イベントオブジェクトのストレージを提供する必要があります。これは常駐している必要があります。 ドライバーによって作成されたデバイスオブジェクトの[デバイス拡張機能](device-extensions.md)、コントローラー[オブジェクト](using-controller-objects.md)を使用している場合はコントローラー拡張機能、ドライバーによって割り当てられた非ページプールを使用できます。

ドライバーが**Keinitializeevent**を呼び出す場合、そのイベントオブジェクトのドライバーの常駐ストレージへのポインターを渡す必要があります。 また、呼び出し元は、イベントオブジェクトの初期状態 (シグナル状態または未シグナル) を指定する必要があります。 また、呼び出し元は、次のいずれかのイベントの種類も指定する必要があります。

-   **同期イベント**

    *同期イベント*がシグナル状態に設定されている場合、イベントが非シグナル状態にリセットされるのを待機している1つのスレッドが実行の対象となり、イベントの状態が自動的に not シグナル状態にリセットされます。

    この種類のイベントは、待機が完了するたびにシグナル状態が自動的にリセットされるため、 *autoclearing イベント*と呼ばれることがあります。

-   **NotificationEvent**

    *通知イベント*がシグナル状態に設定されている場合、イベントを非シグナル状態にリセットするのを待機しているすべてのスレッドが実行の対象となり、シグナル状態になっていないことを明示的にリセットするまで、イベントはシグナル状態のままになります。つまり、指定された*イベント*ポインターを使用して、 [**Keclearevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)または[**KeResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent)が呼び出されています。

デバイスまたは中間のドライバーの中には、ドライバー専用のスレッドが1つしかないものがあります。共有リソースを保護するイベントを待機することによって、操作を同期できるスレッドのセットだけを使用します。

I/o 操作の完了を待機するためにイベントオブジェクトを使用するほとんどのドライバーは、 **Keinitializeevent**を呼び出すと、入力の*種類*を**notificationevent**に設定します。 [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)または[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)でドライバーによって作成される irp 用に設定されたイベントオブジェクトは、呼び出し元がイベントを待機するため、ほとんどの場合、 **notificationevent**として初期化されます。1つ以上の下位レベルのドライバーによって要求が満たされていることを通知します。

ドライバーが自身で初期化された後、ドライバー専用のスレッド (存在する場合) とその他のルーチンがイベントに対する操作を同期できます。 たとえば、システムのフロッピーコントローラードライバーなどの Irp のキューを管理するスレッドがあるドライバーでは、前の図に示すように、イベントの IRP 処理が同期される場合があります。

1.  デバイスでの処理のために IRP をデキューしたスレッドは、初期化されたイベントオブジェクトのドライバー提供のストレージへのポインターを使用して[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出します。

2.  その他のドライバールーチンは、IRP を満たすために必要な i/o 操作をデバイスで実行します。これらの操作が完了すると、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンは、イベントオブジェクトへのポインターを使用して[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)を呼び出します。ドライバーによって決定された優先順位です。スレッド (前の図で示されているように*インクリメント*) のブーストと、ブール値の*待機*が**FALSE**に設定されます。 **KeSetEvent**を呼び出すと、イベントオブジェクトがシグナル状態に設定され、待機中のスレッドの状態が [準備完了] に変わります。

3.  カーネルは、プロセッサが使用可能になるとすぐにスレッドをディスパッチします。つまり、優先度の高い他のスレッドは現在準備完了状態であり、カーネルモードルーチンが上位の IRQL で実行されることはありません。

    *DpcForIsr*が既に Irp で**IoCompleteRequest**を呼び出していない場合、スレッドは irp を完了できるようになりました。また、デバイス上で別の irp をデキューして処理することができます。

*Wait*パラメーターを**TRUE**に設定して**KeSetEvent**を呼び出すと、 **KeSetEvent**から戻ったときに、呼び出し元が[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)または[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)サポートルーチンをすぐに呼び出すことを示します。

*****Wait***パラメーター toKeSetEvent を設定する際には、次のガイドラインを考慮してください。**

IRQL &lt; ディスパッチ\_レベルで実行されるページング可能なスレッドまたはページング可能なドライバールーチンは、 *Wait*パラメーターを**TRUE**に設定して**KeSetEvent**を呼び出すことはできません。 このような呼び出しでは、 **KeSetEvent**と**KeWaitForSingleObject**または**KeWaitForMultipleObjects**の呼び出しの間に呼び出し元がページアウトされた場合に、致命的なページフォールトが発生します。

IRQL = ディスパッチ\_レベルで実行される標準のドライバールーチンは、システムを停止することなく、任意のディスパッチャーオブジェクトで0以外の間隔を待機することはできません。 ただし、このようなルーチンは、ディスパッチ\_レベル以下の IRQL で実行中に**KeSetEvent**を呼び出すことができます。

標準のドライバールーチンを実行する IRQLs の概要については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

**KeResetEvent**は、指定された*イベント*の以前の状態を返します。これは、 **KeResetEvent**への呼び出しが発生したときに、シグナル状態に設定されたかどうかにかかわらず発生します。 **Keclearevent**は、指定された*イベント*の状態を非シグナル状態に設定するだけです。

**上記のサポートルーチンを呼び出すタイミングについては、次のガイドラインを考慮してください。**

パフォーマンスを向上させるには、呼び出し元が**KeResetEvent**から返された情報を取得して次に行う処理を決定しない限り、すべてのドライバーが**Keclearevent**を呼び出す必要があります。

 

 




