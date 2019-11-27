---
title: パケットベース DMA 用のシステム DMA コントローラーのセットアップ
description: パケットベース DMA 用のシステム DMA コントローラーのセットアップ
ms.assetid: 3a646169-1ea3-4844-b771-d08f4ddec460
keywords:
- システム DMA WDK カーネル、パケットベース
- パケットベースの DMA WDK カーネル
- DMA 転送 WDK カーネル、パケットベース
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87946c145368ad58f3122b76b86265d3252a28ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836335"
---
# <a name="setting-up-the-system-dma-controller-for-packet-based-dma"></a>パケットベース DMA 用のシステム DMA コントローラーのセットアップ





[**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)がドライバーの[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンに制御を転送する場合、ドライバーはシステム DMA コントローラーと一連のマップレジスタを "所有" します。 その後、次の図に示すように、ドライバーは転送操作用に DMA コントローラーを設定する必要があります。

![システム dma コントローラーのプログラミングを示す図](images/3dmaptsf.png)

ドライバーに[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンが含まれている場合、 [**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)は、 *Pirp*パラメーターの **&gt;DeviceObject**に対するポインターを*adaptercontrol*ルーチンに渡します。 ただし、ドライバーが Irp の独自のキューを管理している場合、ドライバーは、 *Adaptercontrol*に渡すコンテキストの一部として、現在の irp へのポインターを含める必要があります。

前の図に示すように、ドライバーの*Adaptercontrol*ルーチンは、次のように DMA 転送を設定します。

1.  *Adaptercontrol*ルーチンは、転送を開始するアドレスを取得します。 初期転送が IRP を満たすために必要な場合、 *Adaptercontrol*ルーチンは[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、この DMA 転送のバッファーを記述する**Irp-&gt;mdladdress**の MDL へのポインターを渡します。

    **Mmgetmdlvirtualaddress**は、ドライバーが転送を開始するシステムの物理アドレスのインデックスとして使用できる仮想アドレスを返します。

    IRP に複数の転送操作が必要な場合は、このセクションで後述するように、ドライバーによって更新された開始アドレスが計算されます。

2.  *Adaptercontrol*ルーチンは、 **Mmgetmdlvirtualaddress**によって返されるアドレスまたは手順1で計算されたアドレスを保存します。 このアドレスは、 [**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)の必須パラメーター (*currentva*) です。

3.  *Adaptercontrol*ルーチンは、システム DMA コントローラーを設定するために**maptransfer**を呼び出し、次のパラメーターを指定します。

    -   IoGetDmaAdapter によって返されるアダプターオブジェクトポインター [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)

    -   現在の IRP の**irp&gt;MdlAddress**にあるポインター (*mdl*)

    -   **Allocateadapterchannel**によってドライバーの*adaptercontrol*ルーチンに渡された*mapregisterbase*ハンドル

    -   この値 (*Currentva*) は、これが、IRP の**maptransfer**への最初の呼び出しである場合に、 **Mmgetmdlvirtualaddress**によって返されます。

        それ以外の場合、ドライバーは更新された*Currentva*値を提供し、バッファー内の次の転送操作を開始する場所を示します。

    -   この転送のバイト数を示す変数 (*長さ*) へのポインター

        ドライバーがすべての要求されたデータを**Maptransfer**の1回の呼び出しで転送でき、DMA 操作にデバイス固有の制約がない場合、*長さ*は、ドライバーの i/o スタックの IRP 位置の**長さ**の値に設定できます。 最大バイト数は、( [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返される*numberofmapregisters* \* ページ\_サイズ) にすることができます。 それ以外の場合、ドライバーは、「[転送要求の分割](splitting-dma-transfer-requests.md)」で説明されているように要求を分割する必要があり、その後、現在の IRP に対する**maptransfer**への後続の呼び出しで*長さ*の値を更新する必要があります。

    -   転送操作の方向を示すブール値 (*Writetodevice*) です (システムメモリからデバイスにデータを転送する場合は TRUE)。

    **Maptransfer**は論理アドレスを返します。 システム DMA を使用するドライバーは、この値を無視する必要があります。

4.  *Adaptercontrol*ルーチンは、DMA 操作用にデバイスを設定します。

5.  *Adaptercontrol*ルーチンは、 **KeepObject**を返します。

デバイスが現在の DMA 操作が完了したことを示した場合、ドライバーは、通常、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンから[**flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)を呼び出す必要があります。

*DpcForIsr*ルーチンまたは dma 操作を完了する別のドライバールーチンは、 **flushadapterbuffers**を呼び出して、システム DMA コントローラーにキャッシュされているデータがシステムメモリに読み込まれるか、デバイスに書き込まれるようにします。 また、現在の IRP に対してより多くのデータを転送するようにシステム DMA コントローラーを再実行する必要がある場合も、同じルーチンで**Maptransfer**を呼び出す必要があります。 同様に、各転送操作の後に、 **Flushadapterbuffers**を再度呼び出す必要があります。

ドライバーが現在の IRP に対して2回以上**Maptransfer**を呼び出す必要がある場合、すべての呼び出しで同じアダプターオブジェクトポインター、 *Mdl*ポインター、 *mapregisterbase*ハンドル、および転送方向が提供されます。 ただし、ドライバーは*Currentva*と*長さ*のパラメーターを更新してから、 **maptransfer**の2番目以降の呼び出しを行う必要があります。 これらの各パラメーターの更新された値を計算するには、次の式を使用します。

-   *Currentva* = *currentva* + (前の**maptransfer**への呼び出しで要求された*長さ*)

-   *長さ*= 最小 (転送する残りの**長さ**( **IoGetDmaAdapter**によって返される*NUMBEROFMAPREGISTERS* \* のページ\_サイズ))

各ドライバーが DMA 転送に関して保持するコンテキスト情報は、特定のデバイスのニーズによって異なります。 一般的なコンテキストには、MDL (*Currentva*) の現在の仮想アドレス、これまでに転送されたバイト数、転送する残りのバイト数、現在の IRP へのポインター、およびドライバーライターによって判断されるその他の情報が含まれます。役立つ.

要求された転送が完了した場合、またはドライバーが IRP のエラー状態を返す必要がある場合、ドライバーは[**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)をすぐに呼び出して、他のドライバーおよびこのドライバーが使用するシステム DMA コントローラーを解放する必要があります。

 

 




