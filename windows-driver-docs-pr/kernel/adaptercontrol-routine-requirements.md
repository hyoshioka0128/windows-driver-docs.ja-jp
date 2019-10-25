---
title: AdapterControl ルーチンの要件
description: AdapterControl ルーチンの要件
ms.assetid: 09ce4ad8-eb1b-4fd0-9a22-4249d09584b3
keywords:
- AdapterControl ルーチン、要件
- AdapterControl ルーチン、書き込み
- アダプタオブジェクト WDK カーネル、AdapterControl ルーチンの記述
- DMA が WDK カーネルを転送し、AdapterControl ルーチンを作成する
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62d40d7fdac43e42143ccd8322ba4ee70921b27b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837281"
---
# <a name="adaptercontrol-routine-requirements"></a>AdapterControl ルーチンの要件





少なくとも、 [*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンは次の操作を行う必要があります。

1.  入力*Mapregisterbase*値とその他のコンテキスト情報を保存します。この情報は、ドライバーが現在の IRP に対して1つ以上の DMA 転送操作を実行するために必要です。 各 DMA 転送操作が完了すると、ドライバーは*Mapregisterbase*値を[**flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)に渡す必要があります。

2.  適切な[**IO\_割り当て\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)値を返します。

    -   デバイスが下位デバイスであり、ドライバーがシステム DMA を使用する場合は**KeepObject** 。

    -   **DeallocateObjectKeepRegisters**デバイスがバスマスターの場合、ドライバーはパケットベースのバスマスタ DMA を使用します。

ドライバーの設計によっては、 *adaptercontrol*ルーチンも制御を返す前に、次の操作を実行できます。

1.  デバイスでの転送の開始位置を決定します。

2.  転送の開始位置によってデバイスの制限がある場合に、可能な転送のサイズを計算します。

    一般に、 *Numberofmapregisters*におけるプラットフォーム固有の制限により、転送要求を部分的な転送に分割する必要があるかどうかを判断するために、 [**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出すルーチンの役割を担います。前のセクションで説明した DMA 転送操作ごとに使用でき、[転送要求の分割](splitting-dma-transfer-requests.md)について詳しく説明します。

3.  デバイス (またはコントローラー) 拡張機能で、各転送要求について、ドライバーによって維持される状態を設定します。

    たとえば、 *Adaptercontrol*ルーチンは、ドライバーの DMA 転送操作をタイムアウトにする[*customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンのエントリポイントを使用して[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)を呼び出す場合があります。

4.  **Irp&gt;MdlAddress**で渡された MDL ポインターを使用して[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、転送の開始のインデックスを取得します。 [**maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)に渡すのに適しています。

5.  **Maptransfer**を呼び出して、システム DMA コントローラーを設定するか、バスマスタデバイスの物理-論理アドレスのマッピングを取得します。

6.  [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出すことによって呼び出される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを使用して、転送操作用にドライバーのデバイスをプログラムします。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

転送要求で、現在の IRP を満たすために部分転送操作のシーケンスを実行する必要がある場合、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンは、通常、次のようにデバイスの reprogramming を行います。転送操作。 *Adaptercontrol*ルーチンは、受信転送の IRP ごとに1回だけ呼び出されます。

現在の転送 IRP (通常は*DpcForIsr*または*customdpc*ルーチン) を完了するドライバールーチンも、 [**freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)または[**を呼び出して、システム DMA コントローラーまたはバスマスターアダプターを解放します。FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)。 このドライバールーチンは、最後の部分転送操作が実行されたときに、できるだけ早く適切な呼び出しを行う必要があります。これにより、下位の DMA デバイスのドライバーがシステム DMA コントローラーまたはバスマスタドライバーが次の転送の処理を開始できるようになります。IRP を迅速に行います。

 

 




