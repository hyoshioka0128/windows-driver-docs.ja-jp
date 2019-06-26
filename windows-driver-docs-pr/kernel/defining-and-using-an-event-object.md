---
title: イベント オブジェクトの定義と使用
description: イベント オブジェクトの定義と使用
ms.assetid: 4b7807f0-bbea-4402-b028-9ac73724717f
keywords:
- イベント オブジェクトの WDK カーネル
- イベント オブジェクトを待機しています。
- 同期イベントの WDK カーネル
- 通知イベントの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d4726b782b71c784f60f1e5b682647c4671cb31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377119"
---
# <a name="defining-and-using-an-event-object"></a>イベント オブジェクトの定義と使用





イベント オブジェクトを使用する任意のドライバーを呼び出す必要があります[ **KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializeevent)、 [ **IoCreateNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatenotificationevent)、または[**IoCreateSynchronizationEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesynchronizationevent)設定待機している、前に、クリア、またはイベントをリセットします。 次の図は、同期、スレッドのドライバーがイベント オブジェクトを使用する方法を示します。

![イベント オブジェクトの待機を示す図](images/3evntobj.png)

前の図に示すように、このようなドライバーは、イベント オブジェクトは、常駐である必要があります、記憶域を提供する必要があります。 ドライバーを使用して、[デバイス拡張機能](device-extensions.md)コント ローラーの拡張機能を使用する場合、デバイスのドライバーが作成したオブジェクトの[コント ローラー オブジェクト](using-controller-objects.md)、または、ドライバーによって割り当てられた非ページ プール。

ドライバーを呼び出すと**KeInitializeEvent**、イベント オブジェクトのドライバーの常駐ストレージへのポインターを渡す必要があります。 さらに、呼び出し元は、初期を指定する必要があります (シグナルまたはシグナル状態にならない) の状態イベント オブジェクト。 呼び出し元は、イベントの種類は、次のいずれかを指定する必要があります。

-   **SynchronizationEvent**

    ときに、*同期イベント*設定されているシグナルされた状態にリセットする Not シグナルされたイベントを待機している 1 つのスレッドが実行の対象となり、イベントの状態が Not シグナルされたに自動的にリセットします。

    この種類のイベントとも呼ばれます、 *autoclearing イベント*のシグナルされた状態は、待機が満たされるたびに自動的にリセットするため、します。

-   **NotificationEvent**

    ときに、*通知イベント*はシグナルされた状態に設定すると、Not シグナルされたにリセットされるイベントを待機していたすべてのスレッド実行の対象になり、明示的にリセットするまで、イベントがシグナルされた状態のままNot シグナルが発生します: への呼び出しがある、 [ **KeClearEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keclearevent)または[ **KeResetEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keresetevent)で、指定された*イベント*ポインター。

いくつかのデバイスまたは中間ドライバーは、一連の共有リソースを保護するイベントを待機して、操作を同期する場合がありますのスレッドではおろか、1 つのドライバー専用スレッドがあります。

イベント オブジェクトを使用して、I/O 操作の完了に設定、入力を待機するほとんどのドライバー*型*に**NotificationEvent** 、呼び出すときに**KeInitializeEvent**します。 イベント オブジェクトが、ドライバーを作成する Irp を設定する[ **IoBuildSynchronousFsdRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)または[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)として初期化されるほとんどの場合に、 **NotificationEvent**呼び出し元が 1 つまたは複数の下位レベルのドライバーによって、その要求が満たされている通知のイベントを待つためです。

ドライバーが初期化自体、ドライバー専用のスレッドでは、存在する場合と、イベントでは、その操作を同期できるは、その他のルーチン。 たとえば、システム フロッピー コント ローラー ドライバーなどの Irp でキューを管理するスレッドによるドライバーで前の図に示すように IRP のイベントの処理を同期する可能性があります。

1.  デバイスでの処理の IRP がデキュー、スレッドを呼び出す[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)初期化イベント オブジェクトのドライバーが指定した記憶域へのポインター。

2.  デバイス、IRP を満たすし、これらの操作が完了、ドライバーに必要な I/O 操作を他のドライバー ルーチン実行[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチンの呼び出し[ **KeSetEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)スレッドのイベント オブジェクトへのポインター、ドライバーが決定の優先度を向上させる (*インクリメント*前の図に示すように、)、およびブール値*待機*設定**FALSE**します。 呼び出す**KeSetEvent**イベント オブジェクトを待機しているスレッドの状態を準備完了状態に変更され、シグナルされた状態に設定します。

3.  カーネルは、プロセッサが使用可能なすぐにスレッドの実行をディスパッチします。 つまり、優先度が高いその他のスレッドは現在準備完了状態で、より高い IRQL で実行されるルーチンをカーネル モードではありません。

    スレッドようになりましたことができます IRP を完了する場合、 *DpcForIsr*が呼び出されていない**IoCompleteRequest**既に、IRP におよびデバイスでの処理を別の IRP をデキューすることができます。

呼び出す**KeSetEvent**で、*待機*パラメーターに設定**TRUE**を直ちに呼び出す呼び出し元の意図を示す、 [ **Kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)または[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)から返された場合、ルーチンをサポート**KeSetEvent**します。

**設定の次のガイドラインを考慮して、***待機***パラメーター toKeSetEvent:**

ページング可能なスレッドまたは IRQL で実行されているページング可能なドライバー ルーチン&lt;ディスパッチ\_レベルは呼び出さないで**KeSetEvent**で、*待機*パラメーターに設定**は TRUE。** . 呼び出し元がページ アウト呼び出しの間に発生した場合、このような呼び出しにより、致命的なページ フォールト**KeSetEvent**と**kewaitforsingleobject の 1**または**KeWaitForMultipleObjects**します。

IRQL で実行されている任意の標準のドライバー ルーチン = ディスパッチ\_システム停止することがなくすべてのディスパッチャー オブジェクトに対するレベルを 0 以外の値の間隔を待機できません。 ただし、このようなルーチンを呼び出すことができます**KeSetEvent**ディスパッチに少ないの IRQL で実行中に\_レベル。

実行する標準のドライバー ルーチンで Irql の概要については、次を参照してください。[を管理するハードウェアの優先順位](managing-hardware-priorities.md)します。

**KeResetEvent**の以前の状態を返します、指定された*イベント*: かどうかが設定されているシグナルされたかどうかと呼び出し**KeResetEvent**が発生しました。 **KeClearEvent**の状態を設定するだけ、指定された*イベント*Not シグナル状態にします。

**上記のサポート ルーチンを呼び出すタイミングについては、次のガイドラインを考慮してください。**

パフォーマンスの向上のため、すべてのドライバーを呼び出す必要があります**KeClearEvent** 、呼び出し元によって返される情報を必要がない限り**KeResetEvent**を次に行うことを確認します。

 

 




