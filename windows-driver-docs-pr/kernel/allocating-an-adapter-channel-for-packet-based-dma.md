---
title: パケットベース DMA 用のアダプター チャネルの割り当て
description: パケットベース DMA 用のアダプター チャネルの割り当て
ms.assetid: c95e4b2d-ce19-453a-bcc5-4bb37fc5d9ed
keywords:
- DMA WDK カーネルでは、パケットに基づくシステム
- DMA WDK カーネルのパケットに基づく
- DMA は、パケットに基づく、WDK のカーネルを転送します。
- アダプタのチャネルの割り当てください。
- アダプター チャネル割り当て WDK カーネル
- AllocateAdapterChannel
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 481bb1589c6ca5712d5cffd738f2e05f879cae7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369971"
---
# <a name="allocating-an-adapter-channel-for-packet-based-dma"></a>パケットベース DMA 用のアダプター チャネルの割り当て





準備、DMA パケットに基づくシステムのドライバーの呼び出しに[ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)と[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)受信後、[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)または[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求。

ドライバーは、これらのルーチンを呼び出す前にその[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン (またはその他のルーチンのディスパッチをDMA 転送のハンドル) IRP のパラメーターの有効性をチェックが既に必要があります。 ディスパッチ ルーチンでさらに処理するための別のドライバー ルーチンに IRP がキューにも可能性があります。

ドライバーのルーチンを呼び出す**AllocateAdapterChannel** IRQL で実行する必要があります = ディスパッチ\_レベル。 によって返されるアダプター オブジェクトへのポインターと共に[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)を呼び出すときに、ドライバーは、次を指定する必要があります**AllocateAdapterChannel**:

-   ターゲット デバイスのオブジェクトへのポインター

-   エントリ ポイントの[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)ルーチン

-   コンテキストのドライバーにより決定された情報へのポインター、 *AdapterControl*ルーチンが使用されます

**AllocateAdapterChannel**キュー、ドライバーの*AdapterControl*システム DMA コント ローラーは、このドライバーのセットに割り当てられているときに実行されるルーチン[レジスタにマップ](map-registers.md)が割り当てられましたドライバーの DMA 操作。

開始時、 *AdapterControl*ルーチンを受け取る、*デバイス オブジェクト*と*コンテキスト*への呼び出しで渡されたポインター **AllocateAdapterChannel**、ハンドルと (*MapRegisterBase*) に割り当てられたマップに登録します。

*AdapterControl*ルーチンへのポインターを受け取ることも、**デバイス オブジェクト -&gt;CurrentIrp**ドライバーがある場合、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン。 ドライバーは Irp のキューをそれ自体が管理する場合 (ではなく、 *StartIo*ルーチン) を呼び出すときに渡すコンテキストの一部としてドライバーが IRP が現在へのポインターを含める必要があります**AllocateAdapterChannel**.

*AdapterControl*ルーチンは、次を通常は。

1.  保存または DMA 操作に関するこのドライバーは、どのようなコンテキストを初期化します。 コンテキストは、入力を含めることがあります*MapRegisterBase*ハンドルを渡す必要があります、ドライバー [ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)と[ **FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)と、おそらく、**長さ**I/O から要求された転送の IRP 内の場所をスタックします。

2.  呼び出し[ **MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)続けて**MapTransfer**します。 参照してください[パケットに基づく DMA を設定するシステムの DMA コント ローラー](setting-up-the-system-dma-controller-for-packet-based-dma.md)します。

3.  転送操作を開始する下位のデバイスを設定します。

4.  値を返します**KeepObject**します。

すべて*AdapterControl*ルーチンは、型のシステム定義の値を返す必要があります[ **IO\_割り当て\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_io_allocation_action)します。 DMA では、システムを使用するドライバー、 *AdapterControl*ルーチンは、値を返す必要があります**KeepObject**します。 これにより、システムの DMA コント ローラーの「所有者」を保持するドライバーと、要求されたすべてのデータを転送するまで、マップのレジスタを割り当てられています。

*AdapterControl*ルーチンは、DMA 操作を実行する下位のデバイスを待つことができない各*AdapterControl*ルーチン、する必要があります。 には、少なくとも、次の操作。

1.  コンテキスト情報を保存、特に*MapRegisterBase*ドライバーのデバイスの拡張機能、コント ローラーの拡張機能、またはその他のドライバーにアクセス可能な常駐ストレージ領域に (ドライバーによって割り当てられた非ページ プール) のハンドル。

2.  返す**KeepObject**します。

詳細については、次を参照してください。[書き込み AdapterControl ルーチン](writing-adaptercontrol-routines.md)します。

他のドライバー ルーチン (おそらく、 [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン) 呼び出す必要があります[ **FlushAdapterBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)各 DMA で操作を転送する場合完了しました。 このルーチンも呼び出す必要があります**MapTransfer**と**FlushAdapterBuffers**もう一度は現在 IRP の転送要求を満たすために複数回 DMA コント ローラーを設定するために必要なかどうか。

呼び出す必要がありますが、ドライバーが IRP が現在の要求が満たされると、 [ **FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)します。 最後の呼び出しの直後に続くこのサポート ルーチンを呼び出す必要が**FlushAdapterBuffers** IRP が現在のシステム DMA コント ローラーできる使用可能な (ドライバー) を他の転送要求を満たすように迅速にします。

スキャッター/ギャザー機能との下位のデバイスのドライバーに返す必要がありますも**KeepObject**からその*AdapterControl*ルーチン。 デバイスは、システムの DMA コント ローラーは DMA の操作で、ドライバーは、DMA の特定の要求を分割する必要がありますとの間で行ったりするまで待機できる必要があります。 一部の Windows プラットフォームでこのようなデバイスを転送できます多くて DMA 操作ごとのデータ ページのため、HAL は、そのデバイスのドライバーを 1 つのマップの登録のみを割り当てることができます。

 

 




