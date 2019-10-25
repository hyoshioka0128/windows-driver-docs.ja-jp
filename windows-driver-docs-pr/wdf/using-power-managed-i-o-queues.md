---
title: 電力管理された I/O キューの使用
description: 電力管理された I/O キューの使用
ms.assetid: 271d55ef-d82e-4ffd-bf41-a602c42c3f0e
keywords:
- I/o キュー WDK KMDF、電源管理
- 電源管理 i/o キュー WDK KMDF
- キューへ引数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbcc37ee7e442e07bb4e6965e7b0da4a73c38267
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831971"
---
# <a name="using-power-managed-io-queues"></a>電力管理された I/O キューの使用


ドライバーが i/o キューを作成するときに、キューが*電源管理*されているかどうかを指定できます。 I/o 要求が電源管理キューで使用可能な場合、フレームワークは、デバイスが動作 (D0) 状態にある場合にのみ、ドライバーに要求を配信します。 フレームワークでは、フレームワークが電源管理キューからドライバーに配信したすべての i/o 要求が完了、取り消し、または延期されるまで、デバイスの動作状態を維持することはできません。

電源管理の i/o キューの詳細については、「 [I/o キューの電源管理](power-management-for-i-o-queues.md)」を参照してください。

## <a name="callback-functions-for-power-managed-queues"></a>電源管理キューのコールバック関数


ドライバーで電源管理の i/o キューが使用されている場合は、次の2つのコールバック関数を追加できます。

<a href="" id="---------evtiostop"></a>[*EvtIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)  
[*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)コールバック関数は、指定された i/o 要求の処理を停止します。 デバイスが動作中 (D0) 状態になるか削除されると、ドライバーが所有している要求やドライバーが[所有](request-ownership.md)する要求など、ドライバーが[完了](completing-i-o-requests.md)していないことを示す i/o 要求ごとに、I/o キューの*evtiostop*コールバック関数が1回呼び出されます。i/o ターゲットに[転送](forwarding-i-o-requests.md)されました。

<a href="" id="---------evtioresume"></a>[*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)  
[*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume) callback 関数は、以前に停止された i/o 要求の処理を再開します。 このフレームワークは、デバイスが動作状態に戻った後に、キューからドライバーへの i/o 要求の配信を再開するときに、i/o キューの*EvtIoResume*コールバック関数を呼び出します。

フレームワークがドライバーの[*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)コールバック関数を呼び出すたびに、この関数は通常、i/o 要求を[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)するか、 [**wdfrequeststopacknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)を呼び出して要求の所有権をフレームワークに返します。

この操作は省略可能ですが、一般に、電源管理キューの[*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)コールバック関数を提供する必要があります。 *Evtiostop*を提供することによって、ドライバーは、デバイスとシステムが低電力状態になるまでの時間を短縮するのに役立ちます。

電源管理キューに対して[*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)を指定しなかった場合、このフレームワークは、電源管理キューからドライバーに配信されたすべての要求が完了するまで待機してから、デバイス (またはシステム) を低電力状態にするか、デバイスを削除します。 このように動作しないと、システムが休止状態またはシステムの低電力状態にならない可能性があります。 極端なケースでは、システムがバグチェックコード9F でクラッシュする可能性があります。

ドライバーが i/o ターゲットに要求を転送せず、不確定な時間の要求を保持していない場合は、電源管理キューの[*Evtiostop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)を省略しても問題ありません。

## <a name="waiting-for-dispatcher-objects"></a>ディスパッチャーオブジェクトを待機しています


一般に、ドライバーは、ディスパッチャーオブジェクトを、任意のスレッドコンテキスト内の同期メカニズムとしてのみ使用する必要があります。

[要求ハンドラー](request-handlers.md)は任意のスレッドコンテキストで実行されるため、電源管理キューの要求ハンドラーは、カーネルディスパッチャーオブジェクトが設定されるまで待機することはできません。 そうすると、デッドロックが発生する可能性があります。

ドライバーが dispatcher オブジェクトを待機できるタイミングと、できない場合の対処方法の詳細については、「[カーネルディスパッチャーオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects)」を参照してください。

 

 





