---
title: パケットベース DMA 用のシステム DMA コントローラーのセットアップ
description: パケットベース DMA 用のシステム DMA コントローラーのセットアップ
ms.assetid: 3a646169-1ea3-4844-b771-d08f4ddec460
keywords:
- DMA WDK カーネルでは、パケットに基づくシステム
- DMA WDK カーネルのパケットに基づく
- DMA は、パケットに基づく、WDK のカーネルを転送します。
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d6a2ce4d257115744d0acf1c773ba35bbc0b83
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371231"
---
# <a name="setting-up-the-system-dma-controller-for-packet-based-dma"></a>パケットベース DMA 用のシステム DMA コントローラーのセットアップ





ときに[ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)にドライバーの制御を転送[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control) 、日常的なドライバー「所有」DMA システムコント ローラーと一連のレジスタにマップします。 次に、ドライバーは、次の図に示すように、転送操作では、DMA コント ローラーを設定する必要があります。

![プログラミング システムの dma コント ローラーを示す図](images/3dmaptsf.png)

ドライバーがある場合、 [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン、 [ **AllocateAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)へのポインターを渡す**デバイス オブジェクト&gt;CurrentIrp**で、 *PIrp*パラメーターを*AdapterControl*ルーチン。 渡すコンテキストの一部としてドライバーが IRP が現在へのポインターを含める必要がある場合、ただし、ドライバーは Irp のキューを管理、 *AdapterControl*します。

前図に示すよう、ドライバーの*AdapterControl*ルーチンは次のように、DMA 転送を設定します。

1.  *AdapterControl*ルーチンは、転送を開始する位置のアドレスを取得します。 IRP を満たすために必要な初期転送の*AdapterControl*ルーチンの呼び出し[ **MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)、ポインターで MDL を渡して**Irp -&gt;MdlAddress**、この DMA 転送、バッファーを記述します。

    **MmGetMdlVirtualAddress**ドライバーとして使用できるインデックス システムの物理アドレスの転送を開始位置となる仮想アドレスを返します。

    IRP では、1 つ以上の転送操作が必要とする場合、ドライバーは、このセクションで後述するよう更新された開始アドレスを計算します。

2.  *AdapterControl*ルーチンによって返されるアドレスを保存します**MmGetMdlVirtualAddress**または手順 1. で計算します。 このアドレスは必須パラメーター (*CurrentVa*) に[ **MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer)します。

3.  *AdapterControl*ルーチンの呼び出し**MapTransfer**次のパラメーターを指定して、システム DMA コント ローラーを設定します。

    -   によって返されるアダプター オブジェクト ポインター [ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)

    -   ポインター (*Mdl*) で MDL に**Irp -&gt;MdlAddress**現在 IRP の

    -   *MapRegisterBase*にドライバーのハンドルが渡される*AdapterControl*で日常的な**AllocateAdapterChannel**

    -   値 (*CurrentVa*) によって返される**MmGetMdlVirtualAddress**場合、最初の呼び出しは**MapTransfer** IRP の

        それ以外の場合、ドライバーを提供、更新された*CurrentVa*バッファーの次の転送で操作を開始位置を示す値。

    -   変数へのポインター (*長さ*) この転送バイト数を示す

        ドライバーが 1 回の呼び出しですべての要求されたデータを転送かどうか**MapTransfer** 、DMA 操作でデバイス固有の制約がないと*長さ*の値に設定することができます**長さ**ドライバーの I/O の IRP の場所をスタックします。 長さ (バイト単位) は、最大で (ページ\_サイズ\*、 *NumberOfMapRegisters*によって返される[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter))。 説明したように、要求に分割する必要があります、ドライバーのそれ以外の場合、[転送要求の分割](splitting-dma-transfer-requests.md)の値を更新する必要がありますと*長さ*に後続の呼び出しで**MapTransfer**現在 IRP の。

    -   ブール値 (*WriteToDevice*)、(システム メモリからデータをデバイスに転送) は true、転送操作の方向を示す

    **MapTransfer**論理アドレスを返します。 システム DMA を使用するドライバーには、この値を無視する必要があります。

4.  *AdapterControl*ルーチンは、DMA 操作については、デバイスを設定します。

5.  *AdapterControl*ルーチンを返します。 **KeepObject**します。

デバイスでは、その現在の DMA 操作が完了したことを示します、ドライバーで呼び出す必要があります[ **FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)、通常は、ドライバーから[ *DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン。

*DpcForIsr*ルーチンまたは DMA 操作を完了する別のドライバーのルーチンを呼び出す**FlushAdapterBuffers** DMA システムにキャッシュされているすべてのデータを確実に、コント ローラーがシステム メモリに読み込まれるか、書き込むデバイスです。 同じルーチンも呼び出す必要があります**MapTransfer**もう一度現在 IRP のより多くのデータを転送するシステムの DMA コント ローラーを再設定する必要がある場合。 同様に、呼び出す必要があります**FlushAdapterBuffers**各転送操作をもう一度次です。

場合は、ドライバーを呼び出す必要があります**MapTransfer**同じアダプター オブジェクトのポインターを提供、現在の IRP の 2 回以上*Mdl*ポインター、 *MapRegisterBase*を処理し、すべての呼び出しの方向を転送します。 ただし、ドライバーを更新する必要があります、 *CurrentVa*と*長さ*パラメーターを 2 つ目と、後続の呼び出し前に**MapTransfer**します。 これらの各パラメーターの更新後の値を計算するには、次の数式を使用します。

-   *CurrentVa* = *CurrentVa* + (*長さ*前の呼び出しで要求された**MapTransfer**)

-   *長さ*= 最小 (残り**長さ**転送する (ページ\_サイズ\* *NumberOfMapRegisters*によって返される**IoGetDmaAdapter**))

その DMA の転送に関するコンテキスト情報各ドライバーを維持する必要がありますは、その特定のデバイスのニーズによって異なります。 一般的なコンテキストが MDL に現在の仮想アドレスを含めることがあります (*CurrentVa*)、これまでに転送する可能性がある現在の IRP では、その他の情報へのポインターに残りのバイト数に転送されるバイト数、ドライバー開発者を対象と便利です。

要求された転送が完了すると、またはドライバーを呼び出す必要がある場合は、ドライバーは IRP のエラー状態を返す必要があります、 [ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)他のシステムの DMA コント ローラーを解放するには、すぐにドライバーは、このドライバーを使用します。

 

 




