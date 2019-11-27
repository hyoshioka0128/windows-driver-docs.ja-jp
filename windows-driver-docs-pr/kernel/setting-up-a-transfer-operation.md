---
title: 転送操作のセットアップ
description: 転送操作のセットアップ
ms.assetid: cabac16d-b946-4b96-af2c-5fd0a0d848da
keywords:
- バスマスタ DMA WDK カーネル
- DMA 転送 WDK カーネル、バスマスタ DMA
- アダプタオブジェクト WDK カーネル、バスマスタ DMA
- 論理アドレスの範囲 (WDK DMA)
- WDK DMA に対処する
- 転送操作 WDK DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f488bf04c0bcca185c1264d09337ba6f726d48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838435"
---
# <a name="setting-up-a-transfer-operation"></a>転送操作のセットアップ





[**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)が制御をドライバーの[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンに転送すると、マップレジスタのセットが割り当てられます。 ただし、ドライバーは、次のように、現在の IRP の転送要求のシステム物理メモリを、バスマスターアダプターの論理アドレス範囲にマップする必要があります。

1.  Irp で[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出して、転送を開始する必要があるシステムの物理アドレスのインデックスを取得します。これには、 **Irp-&gt;mdladdress**を使用します。

    戻り値は、 [**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)の必須パラメーター (*currentva*) です。

2.  **Maptransfer**を呼び出して、IRP のバッファーのシステム物理アドレス範囲をバスマスターアダプターの論理アドレス範囲にマップします。

ドライバーは、転送操作用にアダプターを設定できます。 次の図は、転送の設定に関連する手順を示しています。

![転送操作の設定を示す図](images/3dmabus.png)

前の図に示すように、ドライバーの*Adaptercontrol*ルーチンは、次のようにバスマスタ DMA 操作を設定します。

1.  *Adaptercontrol*ルーチンは、転送を開始するアドレスを取得します。 初期転送が IRP を満たすために必要な場合、 *Adaptercontrol*ルーチンは[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、この DMA 転送のバッファーを記述する**Irp-&gt;mdladdress**の MDL へのポインターを渡します。

    **Mmgetmdlvirtualaddress**は、ドライバーが転送を開始するシステムの物理アドレスのインデックスとして使用できる仮想アドレスを返します。

    IRP に複数の転送操作が必要な場合は、このセクションで後述するように、ドライバーによって更新された開始アドレスが計算されます。

2.  *Adaptercontrol*ルーチンは、 **Mmgetmdlvirtualaddress**によって返されるアドレスまたは手順1で計算されたアドレスを保存します。 このアドレスは、 [**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)の必須パラメーター (*currentva*) です。

3.  *Adaptercontrol*ルーチンは**maptransfer**を呼び出します。これは、ドライバーが転送操作を開始するためにバスマスターアダプターをプログラムできる論理アドレスを返します。 **Maptransfer**の呼び出しでは、ドライバーは次のパラメーターを提供します。
    -   IoGetDmaAdapter によって返されるアダプターオブジェクトポインター [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

    -   現在の IRP の**irp&gt;MdlAddress**にある MDL へのポインター

    -   **Allocateadapterchannel**によってドライバーの*adaptercontrol*ルーチンに渡された*mapregisterbase*ハンドル (「 [Bus マスターアダプターオブジェクトの割り当て](allocating-the-bus-master-adapter-object.md)」を参照してください)

    -   現在の IRP に対する**Maptransfer**への最初の呼び出しである場合に、 **Mmgetmdlvirtualaddress**によって返される値。

        それ以外の場合、ドライバーは更新された*Currentva*値を提供します。これは、次に実行する物理-論理マッピングを示します。 (更新された*Currentva*の計算方法については、このセクションで後述します)。

    -   この転送のバイト数を示す変数 (*長さ*) へのポインター

        1つの DMA 操作で要求されたすべてのデータを転送するのに十分なマップレジスタがドライバーにあり、DMA 操作にデバイス固有の制約がない場合、その*長さ*は、ドライバーの i/o スタックの IRP の場所の**長さ**の値に設定できます. 最大で、バイト単位の入力長は、 **IoGetDmaAdapter**によって返される*numberofmapregisters* \* のページ\_サイズにすることができます。 それ以外の場合、ドライバーは、「[転送要求の分割](splitting-dma-transfer-requests.md)」で説明されているように要求を分割する必要があり、その後、現在の IRP に対する**maptransfer**への後続の呼び出しで*長さ*の値を更新する必要があります。

    -   転送操作の方向を示すブール値 (*Writetodevice*) です (メモリからデバイスにデータを転送する場合は TRUE)。

4.  *Adaptercontrol*ルーチンは、DMA 操作用にデバイスを設定します。

5.  *Adaptercontrol*ルーチンは、 **DeallocateObjectKeepRegisters**を返します。

ドライバーが現在の IRP を満たすために**Maptransfer**を2回以上呼び出す必要がある場合、 **maptransfer**を呼び出すたびに同じアダプターオブジェクトポインター、 *Mdl*ポインター、 *mapregisterbase*ハンドル、および転送方向が提供されます。 ただし、ドライバーは、2回目以降の**Maptransfer**への呼び出しで、更新された*Currentva*と*長さ*の値を提供する必要があります。 これらの値を計算するには、次の数式を使用します。

-   *Currentva* = *currentva* + (前の**maptransfer**への呼び出しで要求された*長さ*)

-   *長さ*= 最小 (転送する残りの**長さ**( **IoGetDmaAdapter**によって返される*NUMBEROFMAPREGISTERS* \* のページ\_サイズ))

各ドライバーが DMA 転送に関して保持するコンテキスト情報は、特定のデバイスのニーズによって異なります。 一般的なコンテキストには、MDL (*Currentva*) の現在の仮想アドレス、これまでに転送されたバイト数、転送する残りのバイト数、および場合によっては現在の IRP へのポインターが含まれます。

スキャッター/ギャザー機能を備えたデバイスのドライバーの場合、 **Maptransfer**の*長さ*のパラメーターは入力パラメーターと出力パラメーターの両方になります。 **Maptransfer**から戻ると、システムによってマップされたデータのバイト数が示されます。 つまり、返された論理アドレスと組み合わせた*長さ*の戻り値は、この DMA 操作で転送のこの部分に対してバスマスターアダプターが使用できる論理アドレスの範囲を示します。

**注**   は、 **maptransfer**によって*長さ*が上書きされるので、次の実装ガイドラインに従います。 IRP のドライバーの i/o スタック位置の**長さ**へのポインターを、*長さ*のパラメーターとして渡すことはでき**ません。MapTransfer** (デバイスでスキャッター/ギャザーがサポートされている場合)。

これを行うと、現在の IRP の値が破壊され、ドライバーが要求したすべてのデータを転送したかどうかを判断できなくなる可能性があります。

 

各 DMA 操作の最後に、ドライバーは有効なアダプターオブジェクトポインターを使用して[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)を呼び出し、すべてのデータが転送されたことを確認*し、の*物理-論理マッピングを解放する必要があります。現在の DMA 操作。 ドライバーで、現在の IRP を満たすために追加の DMA 操作を設定する必要がある場合は、各転送操作の完了後に**Flushadapterbuffers**を呼び出す必要があります。

要求されたすべての転送が完了するか、ドライバーが IRP のエラー状態を返す必要がある場合、ドライバーは、 **Flushadapterbuffers**の最後の呼び出しの直後に[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)を呼び出し、バスマスターアダプター。 **FreeMapRegisters**の呼び出しでは、ドライバーは、前の「 **Allocateadapterchannel**」呼び出しで渡されたアダプターオブジェクトポインターを渡す必要があります。

 

 




