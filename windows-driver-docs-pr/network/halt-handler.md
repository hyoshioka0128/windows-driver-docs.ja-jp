---
title: ミニポート ドライバー停止ハンドラー
description: ミニポート ドライバー停止ハンドラー
ms.assetid: 63b0b25e-f52f-4486-a57d-448985207fc8
keywords:
- MiniportHaltEx
- WDK NDIS ハンドラーを停止します。
- アンロードのミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc013a34451cff8c9f193cb1cfcaecf7b9ea892
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374084"
---
# <a name="miniport-driver-halt-handler"></a>ミニポート ドライバー停止ハンドラー





NDIS ミニポート ドライバーを指定する必要があります、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数を[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)します。

*MiniportHaltEx*すべてを元に戻す必要がありますを[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)でした。 たとえば、NDIS ミニポート ドライバーでは次の場合があります。

-   空きポート。 (詳細については、次を参照してください[、NDIS ポートを解放](freeing-an-ndis-port.md)。)。

-   すべてのハードウェア リソースを解放する[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)要求。

-   割り込みのリソースを呼び出すことによって解放[ **NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)します。

-   任意のメモリを解放する[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)割り当てられます。

-   しない限り、NIC を停止、 [ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)関数が、NIC の初期状態に復元既にします。

次の図は、ミニポート ドライバーをアンロードします。

![ミニポート ドライバーをアンロードするかを示す図](images/207-11.png)

*MiniportHaltEx*を返す前に、ドライバーをアンロードするために必要な操作を完了する必要があります。 受信表示の場合、ミニポート ドライバーは未解決 (つまり、受信したネットワーク データがどの NDIS NDIS までことが示されているがまだは返されません)、 *MiniportHaltEx*にこのようなデータが返されるまで戻り、ミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)関数。

上記の図は、一連の呼び出しによって行わでした、 *MiniportHaltEx*関数。 これらの呼び出しにはできても、呼び出しのサブセットのみです。 実際の呼び出しのセットは、ミニポート ドライバーの以前の動作に依存します。 ミニポート ドライバーが作成で呼び出して同じこれら*MiniportInitializeEx*場合ハードウェアの問題のためネットワーク アダプターが正常に初期化することはできませんが、または必要なリソースを取得できないためです。 このような場合は、 *MiniportInitializeEx*先行するアクションを元に戻して、ドライバーをアンロードする必要があります。 それ以外の場合、 *MiniportHaltEx*のアクションは元に戻す*MiniportInitializeEx*します。

次に、ミニポート ドライバーがかかる可能性がある特定のアクションを反転させるために必要な呼び出しについて説明します。

-   ミニポート ドライバーに割り込みが登録されている場合を呼び出す必要が[ **NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)します。

-   呼び出して、ミニポート ドライバーは、タイマーまたはタイマーが設定された場合、 [ **NdisCancelTimerObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)のために作成した各タイマー。 呼び出し**NdisCancelTimerObject**失敗した場合、タイマーが既に発生しました。 ミニポート ドライバーが、タイマーのハンドラーから戻る前に完了するを待機するこの例では、 *MiniportHaltEx*します。

-   ミニポート ドライバーでメモリを割り当てられた場合[ **NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatememorywithtagpriority)を呼び出す必要が[ **NdisFreeMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory)にそのメモリを解放します。

-   ミニポート ドライバーでメモリを割り当てられた場合[ **NdisMAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocatesharedmemory)、または[ **NdisMAllocateSharedMemoryAsyncEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocatesharedmemoryasyncex)、呼び出す必要があります[ **NdisMFreeSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory)そのメモリを解放します。

-   ミニポート ドライバーが割り当てられ初期化とパケットの記述子のプールの記憶域[ **NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)を呼び出す必要が[ **NdisFreeNetBufferPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferpool)をその記憶域を解放します。

-   ミニポート ドライバーでは、割り当てられたまたは任意のハードウェア リソースを予約済み、これらが返されます。 たとえば、ミニポート ドライバーに NIC での I/O ポート範囲がマップされている場合、解除する必要があるポートを呼び出して[ **NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterioportrange)します。

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[NDIS ポートを解放します。](freeing-an-ndis-port.md)

[ミニポート アダプターを停止します。](halting-a-miniport-adapter.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポート ドライバーのリセットと Halt 関数](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






