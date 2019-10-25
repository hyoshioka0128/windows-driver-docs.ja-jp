---
title: ミニポート ドライバー停止ハンドラー
description: ミニポート ドライバー停止ハンドラー
ms.assetid: 63b0b25e-f52f-4486-a57d-448985207fc8
keywords:
- ミニ Porthaltex
- 停止ハンドラー WDK NDIS
- ミニポートドライバーのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4daef1f1cd839ce1e0dea95e0cea9a519ac911a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840486"
---
# <a name="miniport-driver-halt-handler"></a>ミニポート ドライバー停止ハンドラー





NDIS ミニポートドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)に[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を提供する必要があります。

*Miniporthaltex*は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が行ったすべてを元に戻す必要があります。 たとえば、NDIS ミニポートドライバーは次のような場合があります。

-   空きポート。 (詳細については、「 [NDIS ポートの解放](freeing-an-ndis-port.md)」を参照してください)。

-   [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)によって要求されたすべてのハードウェアリソースを解放します。

-   [**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)を呼び出して、割り込みリソースを解放します。

-   [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)に割り当てられたメモリを解放します。

-   [*ミニポート Shutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数が既に nic を初期状態に復元していない限り、nic を停止します。

次の図は、ミニポートドライバーのアンロードを示しています。

![ミニポートドライバーのアンロードを示す図](images/207-11.png)

*ミニ Porthaltex*は、を返す前に、ドライバーをアンロードするために必要な操作を完了する必要があります。 ミニポートドライバーに未処理の受信通知がある場合 (つまり、ndis に示されているものの、どの NDIS がまだ返されていないネットワークデータを受信した場合 *)、ミニ*ポートドライバーの[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数。

上の図は、 *Miniporthaltex*関数によって実行される可能性がある一連の呼び出しを示しています。 これらの呼び出しは、可能な呼び出しのサブセットにすぎません。 実際の呼び出しのセットは、ミニポートドライバーの以前のアクションに依存します。 ハードウェアの問題が原因で、または必要なリソースを取得できないためにネットワークアダプターを正常に初期化できない場合、ミニポートドライバーは*MiniportInitializeEx*で同じ呼び出しを行うことができます。 このような場合、 *MiniportInitializeEx*は、前の操作を元に戻すことによってドライバーをアンロードする必要があります。 それ以外の場合、 *Miniporthaltex*は*MiniportInitializeEx*の操作を元に戻します。

次の一覧では、ミニポートドライバーによって実行される可能性のある特定の操作を取り消すために必要な呼び出しについて説明します。

-   ミニポートドライバーで割り込みが登録されている場合は、 [**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)を呼び出す必要があります。

-   ミニポートドライバーがタイマーまたはタイマーを設定している場合は、作成した各タイマーに対して[**NdisCancelTimerObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)を呼び出す必要があります。 **NdisCancelTimerObject**の呼び出しが失敗した場合、タイマーは既に発生している可能性があります。 この場合、ミニポートドライバーは、タイマーハンドラーが完了するのを待ってから、ミニ*Porthaltex*から戻る必要があります。

-   ミニポートドライバーで[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatememorywithtagpriority)を使用してメモリが割り当てられている場合、そのメモリを解放するには[**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)を呼び出す必要があります。

-   ミニポートドライバーが[**NdisMAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)または[**NdisMAllocateSharedMemoryAsyncEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemoryasyncex)を使用してメモリを割り当てた場合、そのメモリを解放するには[**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)を呼び出す必要があります。

-   [**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)を使用してパケット記述子のプールに対して、ミニポートドライバーによって記憶域が割り当てられ初期化されている場合、その記憶域を解放するには[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)を呼び出す必要があります。

-   ミニポートドライバーにハードウェアリソースが割り当てられているか予約されている場合は、これらが返されます。 たとえば、ミニポートドライバーが NIC の i/o ポート範囲をマップした場合、 [**NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterioportrange)を呼び出すことによってポートを解放する必要があります。

## <a name="related-topics"></a>関連トピック


[ミニポートドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[NDIS ポートの解放](freeing-an-ndis-port.md)

[ミニポートアダプターの停止](halting-a-miniport-adapter.md)

[ミニポートアダプターの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポートドライバーのリセットと停止の機能](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






