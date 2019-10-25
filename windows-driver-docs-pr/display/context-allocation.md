---
title: コンテキストの割り当て
description: コンテキストのコンテキスト保存領域にメモリを割り当てるには、カーネルモードドライバーで DxgkCbCreateContextAllocation を介したコンテキスト割り当てを使用できます。
ms.assetid: DAD08E7F-13F9-4648-A24C-DD9FBA6D490F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce68ab845f35b1d8cc48ad87cf85ce06af446807
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839787"
---
# <a name="context-allocation"></a>コンテキストの割り当て


コンテキストのコンテキスト保存領域にメモリを割り当てるには、カーネルモードドライバーで[*DxgkCbCreateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_createcontextallocation)を介したコンテキスト割り当てを使用できます。 コンテキスト割り当てに新しい機能が追加され、新しいグラフィックスプロセッシングユニット (GPU) 仮想アドレスモデルに適合するようになりました。

## <a name="span-idaccessedphysicallyspanspan-idaccessedphysicallyspanspan-idaccessedphysicallyspanaccessedphysically"></a><span id="AccessedPhysically"></span><span id="accessedphysically"></span><span id="ACCESSEDPHYSICALLY"></span>AccessedPhysically


コンテキスト割り当てでは、 **AccessedPhysically**フラグを指定して、メモリセグメント内で連続して割り当てられるか、システムメモリからアクセスされた場合には絞りにマップする必要があることを示すことができます。

## <a name="span-idassigning_a_gpu_virtual_address_to_a_context_allocationspanspan-idassigning_a_gpu_virtual_address_to_a_context_allocationspanspan-idassigning_a_gpu_virtual_address_to_a_context_allocationspanassigning-a-gpu-virtual-address-to-a-context-allocation"></a><span id="Assigning_a_GPU_virtual_address_to_a_context_allocation"></span><span id="assigning_a_gpu_virtual_address_to_a_context_allocation"></span><span id="ASSIGNING_A_GPU_VIRTUAL_ADDRESS_TO_A_CONTEXT_ALLOCATION"></span>コンテキスト割り当てへの GPU 仮想アドレスの割り当て


ビデオメモリマネージャーは、新しい[*Dxgkcbmapcontextallocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_mapcontextallocation)サービスをカーネルモードドライバーに公開し、GPU 仮想アドレスをコンテキスト割り当てに割り当てます。

コンテキスト割り当ては、指定されたコンテキストに関連付けられているアプリケーション GPU 仮想アドレス空間にマップされます。

コンテキスト割り当てをアプリケーション GPU 仮想アドレス空間に直接マップする場合、ドライバーは特権情報を公開しないよう**に注意する必要が  ます**。

 

これらのサービスは、対応するユーザーモードと同じように動作します。

## <a name="span-idupdating_the_content_of_a_context_allocationspanspan-idupdating_the_content_of_a_context_allocationspanspan-idupdating_the_content_of_a_context_allocationspanupdating-the-content-of-a-context-allocation"></a><span id="Updating_the_content_of_a_context_allocation"></span><span id="updating_the_content_of_a_context_allocation"></span><span id="UPDATING_THE_CONTENT_OF_A_CONTEXT_ALLOCATION"></span>コンテキスト割り当ての内容の更新


場合によっては、カーネルモードドライバーがコンテキスト割り当ての内容を更新する必要があります。 たとえば、特権 (**AccessedPhysically**、GPU 仮想マッピングなし) コンテキスト割り当てには、特定のコンテキストに関連付けられているページディレクトリへの参照を含めることができます。 カーネルモードドライバーに[*DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)によるページディレクトリの再配置が通知された場合、カーネルモードドライバーはそのコンテキスト割り当ての内容を更新することが必要になる場合があります。

このため、新しい[*DxgkCbUpdateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_updatecontextallocation)device driver INTERFACE (DDI) が追加されています。 この DDI は、コンテキスト割り当ての更新を開始するために、ビデオメモリマネージャーに要求をキューに配置します。 更新されるコンテキスト割り当ては、video memory manager ページングプロセスのスクラッチ領域にマップされます。その後、コンテキスト割り当ての実際の更新を行うために、新しい*UpdateContextAllocation*ページング操作でドライバーが呼び出されます。 更新が完了すると、ビデオメモリマネージャーは*DxgkCbUpdateContextAllocation*から戻ります。

カーネルモードドライバーは、 [*DxgkCbUpdateContextAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_updatecontextallocation)の呼び出しと、結果の*UpdateContextAllocation*ページング操作の間で、一部のプライベートドライバーデータを渡すことができます。

 

 





