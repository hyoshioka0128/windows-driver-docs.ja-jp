---
title: AdapterControl ルーチンの記述
description: AdapterControl ルーチンの記述
ms.assetid: a5a7501f-ba4f-441e-be07-6a1b7fac9938
keywords:
- AdapterControl ルーチン、書き込み
- アダプタオブジェクト WDK カーネル、AdapterControl ルーチンの記述
- DMA が WDK カーネルを転送し、AdapterControl ルーチンを作成する
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3688e523d7dae131bce16fda26a0cd5c6f92c5d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835597"
---
# <a name="writing-adaptercontrol-routines"></a>AdapterControl ルーチンの記述





DMA デバイスのほとんどのドライバーには、DMA 操作を開始する[*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンがあります。 ( *Adaptercontrol*ルーチンを必要としないドライバーには、[スキャッター/ギャザー dma を使用](using-scatter-gather-dma.md)するドライバーと[、一般的なバッファー、バスマスタ dma を使用](using-common-buffer-bus-master-dma.md)するドライバーが含まれます)。

ドライバーが[**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出すと、システム dma コントローラーまたはバスマスタアダプターが dma 操作に使用可能な場合、および使用可能なマップレジスタが十分にある場合は、その*adaptercontrol*ルーチンが直ちに実行されます。 それ以外の場合は、これらのリソースが使用可能になるまで、 *Adaptercontrol*ルーチンがキューに登録されます。

ドライバーの*Adaptercontrol*ルーチンから**KeepObject**または**DeallocateObjectKeepRegisters**が返された場合 (これにより、追加の転送操作のためにシステム DMA コントローラーチャネルまたはバスマスターアダプターが保持されます)、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンは、DPC ルーチンが現在の IRP を完了し、制御を返す前に、 [**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)または[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)を呼び出すことによって、アダプターオブジェクトの解放またはレジスタの割り当てを行います。

 

 




