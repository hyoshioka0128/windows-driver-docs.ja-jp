---
title: 共通バッファー システム DMA の使用
description: 共通バッファー システム DMA の使用
ms.assetid: ee060aa4-2db4-4bd2-b107-b71acced97fd
keywords:
- システム DMA WDK カーネルでは、一般的なバッファー
- 一般的なバッファー DMA WDK カーネル
- DMA は、WDK カーネルでは、一般的なバッファーを転送します。
- AllocateCommonBuffer
- 自動初期化モード WDK DMA
- 継続的な DMA WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9aa962faedfdd8fed147bc5910be06237729b95e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361082"
---
# <a name="using-common-buffer-system-dma"></a>共通バッファー システム DMA の使用





システム DMA コント ローラーの自動初期化モードを使用するドライバーは、転送先またはどの DMA を実行するバッファーのメモリを割り当てる必要があります。ドライバー呼び出し[ **AllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff540575)から、通常、このバッファーを取得する、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) 処理ルーチン[**IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 次の図は、ドライバーのバッファーを割り当て、システムの物理メモリにその仮想アドレスの範囲をマップします。

![ドライバーはシステム dma の一般的なバッファーを割り当て方法を示す図](images/3hlsysbf.png)

前の図に示すように、ドライバーはシステム DMA バッファーを割り当てるには、次の手順を受け取ります。

1.  ドライバー呼び出し[ **AllocateCommonBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff540575)、アダプター オブジェクトへのポインターを渡すことによって返された[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)、そのバッファーに対して要求されたバイトの長さ。 経済的なメモリを使用する入力*長さ*値が小さくページをバッファーには、いずれかが必要がありますのする\_サイズ ページの整数倍である必要がありますまたは\_サイズ。

2.  場合**AllocateCommonBuffer**を返します、 **NULL**ポインター、ドライバーする必要がありますは既に要求されている任意のシステム リソースを解放し、状態を返す\_不十分\_内のリソース応答、 **IRP\_MN\_開始\_デバイス**要求。

    それ以外の場合、 **AllocateCommonBuffer**要求されたシステムの仮想アドレス空間内のメモリを割り当てて、そのバッファーへのポインターの 2 つの異なる型を返します。

    -   *LogicalAddress*ドライバーは、記憶域を提供する必要がありますが、その後が無視する必要がありますのバッファー (前の図の BufferLogicalAddress) の

    -   バッファー (前の図の BufferVirtualAddress)、そのバッファーの DMA 操作を記述する、MDL を作成できるようにに、ドライバーも格納する必要がありますの仮想アドレス

    ドライバーでは、デバイスの拡張機能またはその他のドライバーに割り当てられたメモリでこれらのポインターを格納する必要があります。

3.  ドライバー呼び出し[ **IoAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548263) MDL をバッファーを割り当てられません。 ドライバー パス、 *VirtualAddress*によって返されたバッファーの**AllocateCommonBuffer**と*長さ*MDL を割り当てるには、そのバッファーの。

4.  ドライバー呼び出し[ **MmBuildMdlForNonPagedPool** ](https://msdn.microsoft.com/library/windows/hardware/ff554498)によって返されたポインターと**IoAllocateMdl**システムに常駐しているバッファーの仮想アドレスの範囲をマップするには物理メモリです。

一般的なバッファーを割り当てると、その仮想アドレスの範囲のマッピング後、は、下位のデバイスのドライバーは、DMA 転送を要求する IRP の処理を開始できます。 これを行うには、ドライバーは、サポート ルーチンの次の一般的なシーケンスを呼び出します。

1.  ドライバー開発者の裁量により、 [ **RtlMoveMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562030)データをコピーするロックダウン ユーザー バッファーからドライバーに割り当てられた一般的なバッファーの転送をデバイスに

2.  **AllocateAdapterChannel**ドライバーが DMA のデバイスをプログラミングする準備が整うし、システム DMA コント ローラーが必要

3.  [**MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)、MDL バッファーを記述、ドライバーによって割り当てられた共通、転送操作のシステムの DMA コント ローラーを設定するを使用

    ドライバーが呼び出す**MapTransfer**その一般的なバッファーを使用するシステムの DMA コント ローラーを設定する 1 回だけです。 ドライバーを呼び出すことができます、転送中に[ **ReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff560782)バイト数がまま転送して、必要に応じて、呼び出しを確認する**RtlMoveMemory**より多くのデータをコピーするにはユーザー バッファーとの間。

4.  [**FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)ドライバーとの下位のデバイスからその DMA 転送が完了すると

5.  [**FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)ドライバーは IRP をデバイス I/O エラーにより失敗する必要がありますか、要求されたすべてのデータが転送されているようになります

によって返されるアダプター オブジェクト ポインター **IoGetDmaAdapter**にそれぞれの必須のパラメーター以外ルーチンをサポートして**RtlMoveMemory**します。

個々 のドライバーでは、そのデバイスのサービスを提供する各ドライバーの実装方法に応じて、さまざまな時点でこのサポート ルーチンのシーケンスを呼び出します。 たとえば、1 つのドライバーの[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンへの呼び出しを行うことがあります**AllocateAdapterChannel**、別のドライバーは Irp からを削除するルーチンから呼び出しを行うことがありますキュー、ドライバーが作成したインター ロックし、その下位の DMA デバイスでは、データを転送する準備が示されている場合、さらに別のドライバーはこの呼び出しを行うことがあります。

 

 




