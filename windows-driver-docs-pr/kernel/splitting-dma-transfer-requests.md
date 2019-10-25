---
title: DMA 転送要求の分割
description: DMA 転送要求の分割
ms.assetid: 7d5b1649-1021-4876-a9c0-e6b156785ef2
keywords:
- I/o WDK カーネル, 転送要求の分割
- 転送要求の分割
- 転送要求の分割 WDK カーネル
- データ転送 WDK カーネル、分割要求
- データの転送 WDK カーネル、分割要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2397b370ae88a9a941a9b787fc85edd7c7cadf81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836266"
---
# <a name="splitting-dma-transfer-requests"></a>DMA 転送要求の分割





すべてのドライバーは、次のようにして、転送要求を分割し、特定の IRP を満たすために複数の DMA 転送操作を実行することが必要になる場合があります。

-   [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返される[マップレジスタ](map-registers.md)の数

-   IRP のドライバーの i/o スタック位置の**長さ**のメンバーに含まれる転送されるデータのバイト数

-   ドライバーがデータを転送する対象となる、システムの物理メモリ内のページ境界の数

-   ドライバーの DMA 操作に対するデバイス固有の制約。 たとえば、システムの "AT" ディスクドライバーでは、ディスクコントローラーの制限により、256セクターを超える転送要求を分割する必要があります。

ドライバーは、次のように、IRP によって指定されたすべてのデータを転送するために必要なマップレジスタの数を決定できます。

1.  [**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、 **Irp-&gt;MDLADDRESS**の MDL へのポインターを渡して、バッファーの開始仮想アドレスを取得します。 ドライバーは、この仮想アドレスを使用してメモリにアクセスしないようにする必要があることに注意してください。 **Mmgetmdlvirtualaddress**によって返される値は、必ずしも有効なアドレスではなく、MDL のインデックスです。

2.  返されたインデックスと**長さ**の値\_を、IRP のドライバーの i/o スタック位置に渡し、 [ **\_SIZE\_を\_SPAN\_PAGES マクロに**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)渡します。

アドレス\_によって返される値**と\_サイズ\_\_スパンの\_ページ**が、 **IoGetDmaAdapter**によって返される*numberofmapregisters*値より大きい場合、ドライバーは要求されたすべてのデータを転送できません単一の DMA 操作でのこの IRP の場合。 代わりに、次の操作を行う必要があります。

1.  バッファーを、使用可能なマップレジスタ (およびデバイス固有の DMA 制約) の数に合わせてサイズ設定される断片に分割します。

2.  転送要求を満たすために必要な数の DMA 操作を実行します。

たとえば、 **ADDRESS\_と\_SIZE\_を\_\_スパンのページにするとし**ます。これは、転送要求を満たすために12個のマップレジスタが必要であることを示しますが、 *numberofmapregisters*値はによって**返されます。IoGetDmaAdapter**は5つだけです。 (デバイス固有の DMA の制約がないと仮定します)。この場合、ドライバーは3つの DMA 転送操作を実行し、 [**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)を呼び出して、IRP によって要求されたすべてのデータを転送する必要があります。

システムの DMA デバイスドライバーは、1つの i/o 操作で IRP を満たすのに十分なマップレジスタがない場合に、DMA 転送を分割するためにさまざまな手法を使用します。 使用する1つの方法は次のとおりです。

1.  [**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)を呼び出して、ユーザーバッファーの一部を記述する MDL を割り当てます。

2.  [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出して、ユーザーバッファーのその部分をロックダウンします。

3.  バッファーのその部分のデータを転送します。

4.  [**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)を呼び出して、次のいずれかの操作を行います。
    -   手順 1. で割り当てたドライバーが次の転送に十分な大きさの MDL を使用している場合は、 [**mm/** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) * を呼び出して、手順 2. ~ 4. を繰り返します。
    -   それ以外の場合は、 [**Iofreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl)を呼び出し、手順 1. ~ 4. を繰り返します。

5.  すべてのデータが転送されたときに、 [**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)と[**Iofreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreemdl)を呼び出します。

最上位レベルのドライバーが、メモリが制限されているコンピューターの[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を使用してユーザーバッファー全体をロックダウンできない場合は、次の操作を実行できます。

1.  [**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)を呼び出して、部分転送の IRP を割り当て、ユーザーバッファーの一部をロックダウンします。 ロックダウン領域は、通常、**ページ\_サイズ**の倍数か、基になるデバイスの転送容量に合わせてサイズが調整されます。

2.  部分転送の IRP に対して[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出し、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出して、ドライバーが部分転送の irp と関連付けられるように設定されているイベントオブジェクトを待機します。これにより、低いドライバーがステータス\_PENDING を返します。

3.  制御が再び行われたら、すべてのデータが転送されるまで手順 1. と手順 2. を繰り返し、元の IRP を完了します。

ストレージクラスドライバーは、基になる SCSI ポート/ミニポートドライバーに対して大きな転送要求を分割するときに、転送要求の各部分に対して追加の IRP を割り当てます。 ドライバーによって割り当てられた各 IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを登録して、完全転送要求の状態を追跡し、ドライバーによって割り当てられた irp を解放します。 次に、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を使用して、これらの irp をポートドライバーに送信します。

その他のクラス/ポートドライバーは、クラスドライバーがポートドライバーで使用可能なマップレジスタの数を特定できる場合にのみ、この手法を使用できます。 ポートドライバーは、この構成情報をペアのクラスドライバーのレジストリに格納する必要があります。または、ペアリングされたドライバーは、内部デバイス i/o 制御要求を使用してプライベートインターフェイスを定義し、次の数に関する構成情報を渡す必要があります。使用可能なマップは、ポートドライバーからクラスドライバーに登録されます。

1つのモノリシックドライバー (つまり、クラスとポートのペアの一部ではないドライバー) は、それ自体に対して大きな転送要求を分割する必要があります。 このようなドライバーは通常、大きな要求を分割し、IRP を満たすために一連の DMA 操作を実行します。

転送要求が大きすぎて、基になるデバイスドライバーが処理できない場合、上位レベルのドライバーは[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)と[**Iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)を呼び出し、基になるデバイスドライバーに対して部分転送 irp のシーケンスを設定します。

 

 




