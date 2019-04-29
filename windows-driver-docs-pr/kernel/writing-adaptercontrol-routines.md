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
ms.openlocfilehash: 95981bdbe032b437ea7da6976dd003a9abacca30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384538"
---
# <a name="writing-adaptercontrol-routines"></a>AdapterControl ルーチンの記述





DMA デバイスのほとんどのドライバーが、 [ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチンで、DMA 操作の開始を担当します。 (ドライバーを必要としない*AdapterControl*ルーチンを[使用してスキャッター/ギャザー DMA](using-scatter-gather-dma.md)とそれらを[共通バッファー、バス マスター DMA を使用して、](using-common-buffer-bus-master-dma.md))。

ドライバーを呼び出すときに[ **AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)その*AdapterControl* DMA コント ローラーのシステムまたはバス マスター アダプターが利用できる場合、ルーチンがすぐに実行が、DMA 操作、およびレジスタをマップに十分なかどうかは使用できます。 それ以外の場合、 *AdapterControl*ルーチンには、これらのリソースが得られるまではキューに配置します。

場合、ドライバーの*AdapterControl*ルーチンを返します**KeepObject**または**DeallocateObjectKeepRegisters** (のでシステム dma コント ローラーまたは。バス マスター アダプターの追加の転送操作)、ドライバーの[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンマップ、アダプター オブジェクトを解放を呼び出すことによって登録に対して責任[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)または[ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513) DPC する前に日常的な現在の IRP の完了やコントロールを返します。

 

 




