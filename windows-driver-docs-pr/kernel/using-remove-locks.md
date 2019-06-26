---
title: 削除ロックの使用
description: 削除ロックの使用
ms.assetid: 78ca7fe5-ceed-4752-bf1b-d13309097cd8
keywords:
- PnP WDK のロックを解除します。
- ロック ルーチン PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e3fdd7f7345cf9128e4c7b47037e3ba5c705621
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381534"
---
# <a name="using-remove-locks"></a>削除ロックの使用





[削除ロック ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)デバイス、未処理の I/O 操作の数を追跡し、デタッチ、ドライバーのデバイス オブジェクトを削除しても安全な場合を決定する方法を提供します。 システムは、独自の追跡メカニズムを実装する代わりに、ドライバー作成者にこれらのルーチンを提供します。

ドライバーは、2 つの目的はこのメカニズムを使用できます。

1.  ドライバーのことを確認する[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは完了しません、 [ **IRP\_MN\_削除\_デバイス** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) (たとえば、別のドライバーのルーチンは、デバイスにアクセスする) 中に、ロックが保持されているときに要求します。

2.  なぜ、ドライバーがそのデバイス オブジェクトを削除しないでください理由の数をカウントし、そのカウントがゼロになったときにイベントを設定するには。

削除ロックを初期化するために、ドライバーを割り当てる必要があります、 **IO\_削除\_ロック**構造体の[デバイス拡張機能](device-extensions.md)を呼び出して[ **IoInitializeRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeremovelock)します。 通常、ドライバーを呼び出します**IoInitializeRemoveLock**でその[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device) 、日常的な場合、ドライバーを初期化しますデバイス オブジェクトのデバイスの拡張機能の残りの部分。

ドライバーを呼び出す必要があります[ **IoAcquireRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)たびに、I/O 操作を開始します。 ドライバーを呼び出す必要があります[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock) I/O 操作を終了するたびにします。 ドライバーは、2 回以上、ロックを取得できます。 削除ロックのルーチンでは、ロックの未処理の買収のカウントを保持します。 呼び出しごとに**IoAcquireRemoveLock** 、カウントをインクリメントし、 **IoReleaseRemoveLock**デクリメント カウントします。

ドライバーは呼び出す必要がありますも**IoAcquireRemoveLock**にパスとそのコードへの参照を (タイマー、Dpc、コールバック、およびなど) 用です。 ドライバーから呼び出す必要があります**IoReleaseRemoveLock**イベントが返される場合。

場合は、そのディスパッチ コードで[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)、ドライバーがもう一度ロックする必要がありますを呼び出して[ **IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelockandwait)します。 このルーチンでは、ロックのすべての未処理買収がリリースされるまでは返されません。 キューに置かれた I/O 操作が完了するには、各ドライバーを呼び出す必要があります**IoReleaseRemoveLockAndWait** *後*を渡す、 **IRP\_MN\_削除\_デバイス**、次の下位ドライバーへの要求と*する前に*呼び出し、メモリを解放[ **IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)、または呼び出し[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)します。 後**IoReleaseRemoveLockAndWait**のすべての呼び出しに、特定の削除ロックが呼び出された**IoAcquireRemoveLock**同じ削除ロックは失敗します。

後**IoReleaseRemoveLockAndWait**返します、ドライバーは、デバイスでは、削除する準備ができて、状態であることを検討する必要があり、I/O 操作を実行することはできません。 したがって、ドライバーを呼び出す必要がありますいない**IoInitializeRemoveLock**削除ロックの再初期化をします。 ドライバーはによって検証されているときに、この規則違反[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)バグ チェックが発生します。

ドライバーが格納されるため、 **IO\_削除\_ロック**の処理中にドライバーがデバイスの拡張機能を削除するときに削除ロックが削除されたデバイスのデバイスの拡張機能の構造がオブジェクト**IRP\_MN\_削除\_デバイス**要求。

 

 




