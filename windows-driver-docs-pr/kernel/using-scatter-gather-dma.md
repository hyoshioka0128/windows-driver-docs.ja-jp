---
title: スキャッター/ギャザー DMA の使用
description: スキャッター/ギャザー DMA の使用
ms.assetid: dacc618f-d4d4-4c3c-a18c-baeef779e931
keywords:
- AdapterListControl ルーチン
- スキャッター/ギャザー DMA WDK i/o
- PutScatterGatherList
- GetScatterGatherList
- DMA 転送 WDK カーネル、スキャッター/ギャザー DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf5cadf5c8f33c6af38f4d30a497a0ffaa100ade
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835871"
---
# <a name="using-scattergather-dma"></a>スキャッター/ギャザー DMA の使用





システムまたはバスマスタのパケットベースの DMA を実行するドライバーは、特にスキャッター/ギャザー DMA 用に設計されたサポートルーチンを使用できます。 「[パケットベースのシステム dma](using-packet-based-system-dma.md)と[パケットベースのバスマスタ dma](using-packet-based-bus-master-dma.md)の使用」で説明されているルーチンのシーケンスを呼び出す代わりに、ドライバーは[**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)と[**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)を使用できます。

デバイスは、これらのルーチンを使用するために、ドライバーが組み込みのスキャッター/ギャザーサポートを持っている必要はありません。

パケットベースの DMA を使用するドライバーは、スキャッター/ギャザー操作のための次の一般的なサポートルーチンを呼び出します。

1.  **GetScatterGatherList**の呼び出しでパラメーターとして必要な、MDL へのインデックスを取得するための[**Mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

2.  [**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)ドライバーが dma 用にデバイスをプログラミングする準備ができており、システム dma コントローラーまたはバスマスタアダプターが必要な場合

    **GetScatterGatherList**は、システム DMA コントローラーまたはバスマスタアダプターを割り当てて、必要なマップレジスタの数を特定し、それを割り当てて、スキャッター/ギャザーリストに入力し、ドライバーの[*AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)ルーチンを呼び出します。DMA コントローラー、アダプター、およびマップレジスタを使用できます。

3.  要求されたすべてのデータが転送されるか、デバイス i/o エラーが原因でドライバーが IRP に失敗するとすぐに[**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list) 。

    **PutScatterGatherList**は、アダプターバッファーをフラッシュし、マップレジスタを解放して、スキャッター/ギャザーリストを解放します。 ドライバーは、バッファー内のデータにアクセスする前に**PutScatterGatherList**を呼び出す必要があります。

**IoGetDmaAdapter**によって返されるアダプターオブジェクトのポインターは、 **Mmgetmdlvirtualaddress**を除き、これらの各ルーチンに必須のパラメーターです。この場合、 *Irp*-&gt;**mdladdress**にある MDL へのポインターが必要です。

**GetScatterGatherList**ルーチンには、 **Allocateadapterchannel**と**maptransfer**の呼び出しが含まれているので、ドライバーはこれらの呼び出しを行う必要はありません。 ルーチンは、次のパラメーターをパラメーターとして受け取ります。

-   [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)によって返される[**DMA\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)構造体へのポインター

-   DMA 操作の対象デバイスオブジェクトへのポインター

-   *Irp*-&gt;**mdladdress**のバッファーを記述する MDL へのポインター

-   Mdl によって記述されるバッファー内の現在の仮想アドレスへのポインター

-   マップするバイト数

-   転送を実行する[*AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)ルーチンへのポインター

-   *AdapterListControl*ルーチンに渡されるドライバー定義のコンテキスト領域へのポインター。

-   ブール値: デバイスへの転送の場合は**TRUE**です。それ以外の場合は**FALSE**

必要なマップレジスタの数を決定した後、アダプターチャネルとマップレジスタを割り当て、スキャッター/ギャザーリストを入力して転送を準備すると、 **GetScatterGatherList**はドライバーが提供する AdapterListControl を呼び出します。ルーチン。 *AdapterListControl*ルーチンは、IRQL = ディスパッチ\_レベルで任意のスレッドコンテキストで実行されます。

**GetScatterGatherList**への呼び出しでドライバーが提供する*AdapterListControl*ルーチンは、次の重要な点で**allocateadapterchannel**に渡される[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンとは異なります。

-   *AdapterListControl*ルーチンには戻り値はありませんが、 *Adaptercontrol*ルーチンは[**IO\_割り当て\_アクション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action)を返します。

-   *AdapterListControl*ルーチンの3番目のパラメーターは、システムによって割り当てられたマップレジスタの*mapregisterbase*へのポインターではなく、[**散布\_\_図**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_scatter_gather_list)をポイントし、ドライバーは DMA を実行できます。

-   *AdapterListControl*ルーチンは、 *adaptercontrol*ルーチンで必要とされるタスクのサブセットを実行します。

    *AdapterListControl*ルーチンは、 **Allocateadapterchannel**または**maptransfer**を呼び出しません。 その唯一の責任は、入力のスキャッター/ギャザーリストポインターを保存し、そのデバイスを設定し、スキャッター/ギャザーリストを使用して DMA を実行することです。

スキャッター/ギャザーリスト構造には、\_要素の配列と配列内の要素の数を**集める散布図\_** が含まれています。 配列の各要素は、物理的に連続するスキャッター/ギャザー領域の長さと開始物理アドレスを提供します。 ドライバーは、データ転送の長さとアドレスを使用します。

ドライバーは、デバイスがスキャッター/ギャザー DMA をサポートしているかどうかに関係なく、 **GetScatterGatherList**を使用できます。 スキャッター/ギャザー DMA がサポートされていないデバイスの場合、スキャッター/ギャザーリストには要素が1つだけ含まれます。

スキャッター/ギャザールーチンを使用すると、 **Allocateadapterchannel**の呼び出しでパフォーマンスを向上させることができます (前述の「[パケットベースのシステム dma の使用](using-packet-based-system-dma.md)」および「[パケットベースのバスマスタ DMA の使用](using-packet-based-bus-master-dma.md)」で説明しています)。 **Allocateadapterchannel**の呼び出しとは異なり、一度に1つのデバイスオブジェクトに対して複数の**GetScatterGatherList**の呼び出しをキューに入れることができます。 ドライバーは、 *AdapterListControl*ルーチンの実行が完了する前に、同じドライバーオブジェクトで別の DMA 操作に対して**GetScatterGatherList**を再度呼び出すことができます。

ドライバーによって提供された*AdapterListControl*ルーチンから戻ると、 **GetScatterGatherList**はマップレジスタを保持しますが、DMA アダプター構造体は解放されます。

ドライバーが現在の IRP の転送要求を満たしているか、デバイスまたはバス i/o エラーが原因で IRP を失敗させる必要がある場合、バッファー内の転送されたデータにアクセスするには、 **PutScatterGatherList**を呼び出す必要があります。 **PutScatterGatherList**は、アダプターバッファーをフラッシュし、マップレジスタとスキャッター/gather リストを解放します。

 

 




