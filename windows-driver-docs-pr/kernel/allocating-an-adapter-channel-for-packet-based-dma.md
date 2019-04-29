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
ms.openlocfilehash: 56986dd49aa3293cefa8c4774ad9cb0d28b2a2b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326062"
---
# <a name="allocating-an-adapter-channel-for-packet-based-dma"></a>パケットベース DMA 用のアダプター チャネルの割り当て





準備、DMA パケットに基づくシステムのドライバーの呼び出しに[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)と[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)受信後、[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)または[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)要求。

ドライバーは、これらのルーチンを呼び出す前にその[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン (またはその他のルーチンのディスパッチをDMA 転送のハンドル) IRP のパラメーターの有効性をチェックが既に必要があります。 ディスパッチ ルーチンでさらに処理するための別のドライバー ルーチンに IRP がキューにも可能性があります。

ドライバーのルーチンを呼び出す**AllocateAdapterChannel** IRQL で実行する必要があります = ディスパッチ\_レベル。 によって返されるアダプター オブジェクトへのポインターと共に[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)を呼び出すときに、ドライバーは、次を指定する必要があります**AllocateAdapterChannel**:

-   ターゲット デバイスのオブジェクトへのポインター

-   エントリ ポイントの[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチン

-   コンテキストのドライバーにより決定された情報へのポインター、 *AdapterControl*ルーチンが使用されます

**AllocateAdapterChannel**キュー、ドライバーの*AdapterControl*システム DMA コント ローラーは、このドライバーのセットに割り当てられているときに実行されるルーチン[レジスタにマップ](map-registers.md)が割り当てられましたドライバーの DMA 操作。

開始時、 *AdapterControl*ルーチンを受け取る、*デバイス オブジェクト*と*コンテキスト*への呼び出しで渡されたポインター **AllocateAdapterChannel**、ハンドルと (*MapRegisterBase*) に割り当てられたマップに登録します。

*AdapterControl*ルーチンへのポインターを受け取ることも、**デバイス オブジェクト -&gt;CurrentIrp**ドライバーがある場合、 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。 ドライバーは Irp のキューをそれ自体が管理する場合 (ではなく、 *StartIo*ルーチン) を呼び出すときに渡すコンテキストの一部としてドライバーが IRP が現在へのポインターを含める必要があります**AllocateAdapterChannel**.

*AdapterControl*ルーチンは、次を通常は。

1.  保存または DMA 操作に関するこのドライバーは、どのようなコンテキストを初期化します。 コンテキストは、入力を含めることがあります*MapRegisterBase*ハンドルを渡す必要があります、ドライバー [ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)と[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)と、おそらく、**長さ**I/O から要求された転送の IRP 内の場所をスタックします。

2.  呼び出し[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)続けて**MapTransfer**します。 参照してください[パケットに基づく DMA を設定するシステムの DMA コント ローラー](setting-up-the-system-dma-controller-for-packet-based-dma.md)します。

3.  転送操作を開始する下位のデバイスを設定します。

4.  値を返します**KeepObject**します。

すべて*AdapterControl*ルーチンは、型のシステム定義の値を返す必要があります[ **IO\_割り当て\_アクション**](https://msdn.microsoft.com/library/windows/hardware/ff550534)します。 DMA では、システムを使用するドライバー、 *AdapterControl*ルーチンは、値を返す必要があります**KeepObject**します。 これにより、システムの DMA コント ローラーの「所有者」を保持するドライバーと、要求されたすべてのデータを転送するまで、マップのレジスタを割り当てられています。

*AdapterControl*ルーチンは、DMA 操作を実行する下位のデバイスを待つことができない各*AdapterControl*ルーチン、する必要があります。 には、少なくとも、次の操作。

1.  コンテキスト情報を保存、特に*MapRegisterBase*ドライバーのデバイスの拡張機能、コント ローラーの拡張機能、またはその他のドライバーにアクセス可能な常駐ストレージ領域に (ドライバーによって割り当てられた非ページ プール) のハンドル。

2.  返す**KeepObject**します。

詳細については、次を参照してください。[書き込み AdapterControl ルーチン](writing-adaptercontrol-routines.md)します。

他のドライバー ルーチン (おそらく、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン) 呼び出す必要があります[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)各 DMA で操作を転送する場合完了しました。 このルーチンも呼び出す必要があります**MapTransfer**と**FlushAdapterBuffers**もう一度は現在 IRP の転送要求を満たすために複数回 DMA コント ローラーを設定するために必要なかどうか。

呼び出す必要がありますが、ドライバーが IRP が現在の要求が満たされると、 [ **FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)します。 最後の呼び出しの直後に続くこのサポート ルーチンを呼び出す必要が**FlushAdapterBuffers** IRP が現在のシステム DMA コント ローラーできる使用可能な (ドライバー) を他の転送要求を満たすように迅速にします。

スキャッター/ギャザー機能との下位のデバイスのドライバーに返す必要がありますも**KeepObject**からその*AdapterControl*ルーチン。 デバイスは、システムの DMA コント ローラーは DMA の操作で、ドライバーは、DMA の特定の要求を分割する必要がありますとの間で行ったりするまで待機できる必要があります。 一部の Windows プラットフォームでこのようなデバイスを転送できます多くて DMA 操作ごとのデータ ページのため、HAL は、そのデバイスのドライバーを 1 つのマップの登録のみを割り当てることができます。

 

 




