---
title: コンテキストの割り当て
description: 領域のコンテキストの保存されたコンテキストのメモリを割り当て、カーネル モード ドライバーは DxgkCbCreateContextAllocation を使用してコンテキストの割り当てを使用できます。
ms.assetid: DAD08E7F-13F9-4648-A24C-DD9FBA6D490F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2124558087b5d39520be84093f3b91c2343f7d4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535626"
---
# <a name="context-allocation"></a>コンテキストの割り当て


領域のコンテキストの保存されたコンテキストのメモリを割り当てるには、カーネル モード ドライバーがコンテキストの割り当てを使用してを使用できます[ *DxgkCbCreateContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/hh451312)します。 させることに適合、新しいグラフィックス処理装置 (GPU) の仮想アドレス モデルのコンテキストの割り当てに新しい機能が追加されます。

## <a name="span-idaccessedphysicallyspanspan-idaccessedphysicallyspanspan-idaccessedphysicallyspanaccessedphysically"></a><span id="AccessedPhysically"></span><span id="accessedphysically"></span><span id="ACCESSEDPHYSICALLY"></span>AccessedPhysically


コンテキストの割り当てを指定できます、 **AccessedPhysically**割り当てを連続して割り当てられたメモリのセグメントでまたはシステム メモリからアクセスする場合は、開口部にマップすることを示すフラグ。

## <a name="span-idassigningagpuvirtualaddresstoacontextallocationspanspan-idassigningagpuvirtualaddresstoacontextallocationspanspan-idassigningagpuvirtualaddresstoacontextallocationspanassigning-a-gpu-virtual-address-to-a-context-allocation"></a><span id="Assigning_a_GPU_virtual_address_to_a_context_allocation"></span><span id="assigning_a_gpu_virtual_address_to_a_context_allocation"></span><span id="ASSIGNING_A_GPU_VIRTUAL_ADDRESS_TO_A_CONTEXT_ALLOCATION"></span>コンテキストの割り当てへの GPU の仮想アドレスの割り当てください。


ビデオ メモリ マネージャーは、新しい公開[ *DxgkCbMapContextAllocation* ](https://msdn.microsoft.com/library/windows/hardware/dn906334)サービス コンテキストの割り当てに GPU 仮想アドレスを割り当てることのカーネル モード ドライバーをします。

コンテキストの割り当ては、指定したコンテキストに関連付けられているアプリケーションの GPU 仮想アドレス空間にマップされます。

**注**  ドライバーはコンテキストの割り当てが、アプリケーションの GPU 仮想アドレス空間に直接マップするときに特権情報を公開しないように注意する必要があります。

 

これらのサービスは、ユーザー モードの対応するように動作します。

## <a name="span-idupdatingthecontentofacontextallocationspanspan-idupdatingthecontentofacontextallocationspanspan-idupdatingthecontentofacontextallocationspanupdating-the-content-of-a-context-allocation"></a><span id="Updating_the_content_of_a_context_allocation"></span><span id="updating_the_content_of_a_context_allocation"></span><span id="UPDATING_THE_CONTENT_OF_A_CONTEXT_ALLOCATION"></span>コンテキストの割り当てのコンテンツの更新


コンテキストの割り当てのコンテンツを更新する、カーネル モード ドライバーに必要なしばらくかもしれません。 特権など (**AccessedPhysically**GPU の仮想マッピングなし) のコンテキストの割り当ては、特定のコンテキストに関連付けられているページのディレクトリへの参照を含めることができます。 によってページ ディレクトリの再配置のカーネル モード ドライバーが通知されるタイミング[ *DxgkDdiSetRootPageTable*](https://msdn.microsoft.com/library/windows/hardware/dn906342)、カーネル モード ドライバーは、そのコンテキストの割り当てのコンテンツを更新する必要があります。

この目的で、新しい[ *DxgkCbUpdateContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/dn906336)デバイス ドライバー インターフェイス (DDI) を追加します。 この DDI はキューのコンテキストの割り当ての更新プログラムを開始するには、ビデオ メモリ マネージャーに要求します。 更新されているコンテキストの割り当ては、ビデオ メモリ マネージャー ページング プロセスのスクラッチ領域にマップし、新しいドライバーと呼ばれる*UpdateContextAllocation*ページング操作コンテキストの実際の更新を実行するには割り当てです。 ビデオ メモリ マネージャーが返す*DxgkCbUpdateContextAllocation*更新が完了した後。

カーネル モード ドライバーがその呼び出しの間で一部のドライバーのプライベート データを渡すことができます[ *DxgkCbUpdateContextAllocation* ](https://msdn.microsoft.com/library/windows/hardware/dn906336)および結果*UpdateContextAllocation*ページング操作です。

 

 





