---
title: AdapterControl ルーチンの記述
description: AdapterControl ルーチンの記述
ms.assetid: a5a7501f-ba4f-441e-be07-6a1b7fac9938
keywords:
- 書き込みの AdapterControl ルーチン
- アダプター オブジェクトの WDK カーネル、AdapterControl ルーチンを記述
- AdapterControl ルーチンを記述、DMA 転送 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2086aefeb60e8d10f2063b0886ed5c2a8950e6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374144"
---
# <a name="writing-adaptercontrol-routines"></a>AdapterControl ルーチンの記述





DMA デバイスのほとんどのドライバーが、 [ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)ルーチンで、DMA 操作の開始を担当します。 (ドライバーを必要としない*AdapterControl*ルーチンを[使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)とそれらを[共通バッファー、バス マスター DMA を使用して、](using-common-buffer-bus-master-dma.md))。

ドライバーを呼び出すときに[ **AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)その*AdapterControl* DMA コント ローラーのシステムまたはバス マスター アダプターが利用できる場合、ルーチンがすぐに実行が、DMA 操作、およびレジスタをマップに十分なかどうかは使用できます。 それ以外の場合、 *AdapterControl*ルーチンには、これらのリソースが得られるまではキューに配置します。

場合、ドライバーの*AdapterControl*ルーチンを返します**KeepObject**または**DeallocateObjectKeepRegisters** (のでシステム dma コント ローラーまたは。バス マスター アダプターの追加の転送操作)、ドライバーの[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチンマップ、アダプター オブジェクトを解放を呼び出すことによって登録に対して責任[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)または[ **FreeMapRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers) DPC する前に日常的な現在の IRP の完了やコントロールを返します。

 

 




