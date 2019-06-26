---
title: DMA 転送要求の分割
description: DMA 転送要求の分割
ms.assetid: 7d5b1649-1021-4876-a9c0-e6b156785ef2
keywords:
- I/O WDK カーネルでは、転送要求を分割
- 分割の転送要求
- 譲渡要求は WDK カーネルの分割
- データ転送の要求を分割、WDK のカーネル
- データ WDK カーネルでは、分割要求を転送します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f5980a2e3fc2a8a887673415e26ef0e6889301
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383002"
---
# <a name="splitting-dma-transfer-requests"></a>DMA 転送要求の分割





すべてのドライバーは、転送要求を分割によっては、次の特定の IRP を満たすために、1 つ以上の DMA 転送操作を実行する必要があります。

-   数[レジスタにマップ](map-registers.md)によって返される[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)

-   転送されるデータのバイト数に含まれる、**長さ**IRP のドライバーの I/O スタックの場所のメンバー

-   ドライバーがデータを転送するには先、または元のバッファーのシステムの物理メモリ内でのページ境界の数

-   ドライバーの DMA 操作でデバイス固有の制約。 たとえば、「アット」ディスク ドライバー システムは、256 個を超えるセクター ディスク コント ローラーの制限のための転送要求を分割する必要があります。

ドライバーは IRP で次のように指定されたすべてのデータを転送するために必要なマップのレジスタの数を特定できます。

1.  呼び出す[ **MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で MDL にポインターを渡す**Irp の&gt;MdlAddress**バッファーの開始仮想アドレスを取得します。 ドライバーがこの仮想アドレスを使用してメモリへのアクセスを試みる必要がありますいないに注意してください。 によって返される値**MmGetMdlVirtualAddress** MDL、必ずしも有効なアドレスへのインデックスします。

2.  返されるインデックスとの値を渡す**長さ**ドライバーの I/O でスタックに IRP の場所、 [**アドレス\_AND\_サイズ\_TO\_スパン\_ページ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロ。

値がによって返される場合**アドレス\_AND\_サイズ\_TO\_スパン\_ページ**がより大きい、 *NumberOfMapRegisters*値によって返される**IoGetDmaAdapter**ドライバーは、単一の DMA 操作では、この IRP の要求されたすべてのデータを転送することはできません。 代わりに、次の方法にする必要があります。

1.  バッファーが使用可能なマップのレジスタ (および、そのデバイスに固有の DMA 制約) の数に合わせて設定されている部分に分割します。

2.  転送要求を満たすために多くの DMA 操作を実行します。

たとえば、**アドレス\_AND\_サイズ\_TO\_スパン\_ページ**12 個のマップのレジスタは、譲渡要求が、を満たすために必要であることを示します。*NumberOfMapRegisters*によって返される値**IoGetDmaAdapter**は 5 つのみです。 (と仮定しないデバイスに固有の DMA 制約。)ここでは、ドライバーを呼び出す DMA 転送の 3 つの操作する必要があります実行[ **MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer) IRP から要求されたすべてのデータを転送する 3 回です。

システムの DMA のデバイス ドライバーは、単一の I/O 操作には IRP を満たすために十分なマップのレジスタがある場合、DMA の転送を分割するさまざまな手法を使用します。 1 つの方法を使用して、次に示します。

1.  呼び出す[ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)ユーザー バッファーの一部を説明する、MDL を割り当てることです。

2.  呼び出す[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)ユーザー バッファーの部分をロックダウンします。

3.  バッファーの部分のデータを転送します。

4.  呼び出す[ **MmUnlockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)し、次のいずれかの操作を行います。
    -   手順 1 で、ドライバーが割り当てられている MDL が転送の次のコンポーネントに対して十分な大きさの場合は、呼び出す[ **MmPrepareMdlForReuse** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)手順 2 ~ 4 を繰り返します。
    -   それ以外の場合、呼び出す[ **IoFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)手順 1. ~ 4. を繰り返します。

5.  呼び出す[ **MmUnlockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpages)と[ **IoFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreemdl)すべてのデータが転送されたとき。

最上位レベルのドライバーの全体のユーザー バッファーできませんロックダウン[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)限られたメモリ使用のマシンで、次の操作ができます。

1.  呼び出す[ **IoBuildSynchronousFsdRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)部分転送 IRP およびロック ダウン ユーザー バッファーの一部を割り当てます。 ロックされた領域は、の倍数では、通常**ページ\_サイズ**または基になるデバイスの転送の容量に合わせてサイズです。

2.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)の部分的な転送、IRP と呼び出し[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)イベント オブジェクトを待機する、下位のドライバーが状態を返す場合、その部分転送 IRP に関連するセットアップ ドライバー\_保留します。

3.  手順 1 と 2 まで、データを転送すると、すべてを制御します。 を再びときに、次に、元の IRP を完了します。

ストレージ クラス ドライバーは、基になる SCSI ポート/ミニポート ドライバーの大きな転送要求を分割、転送要求の各部分の追加の IRP が割り当てられます。 登録、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)各ドライバーに割り当てられた IRP、完全転送要求の状態を追跡し、ドライバーによって割り当てられた Irp を解放するための日常的な。 送信これら Irp ポート ドライバーを使用して、ログオンし、 [**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

その他のクラス/ポート ドライバーがこの手法を使用できるは、クラス ドライバーがマップの数を決定することができる場合にのみレジスタがポート ドライバーを使用します。 ポートのドライバーは、ペアになっているクラス ドライバーのレジストリでこの構成情報を格納する必要があるか、ペアになっているドライバーの数に関する構成情報を渡す内部デバイス I/O 制御の要求を使用して、プライベート インターフェイスを定義する必要があります。クラスのドライバーにポート ドライバーから使用可能なマップを登録します。

DMA デバイス用のモノリシックなドライバー (つまり、ドライバー クラスとポートのペアの一部ではない) は、自身の大きな転送要求を分割する必要があります。 このようなドライバーは通常の部分に大きな要求を分割して、IRP を満たすために一連の DMA 操作を実行します。

高度なドライバーを呼び出すことができる場合、譲渡要求が大きすぎて、基になるデバイス ドライバーを処理するのに[ **MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)と[ **IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)、部分的な転送 Irp の基になるデバイス ドライバーのシーケンスを設定します。

 

 




