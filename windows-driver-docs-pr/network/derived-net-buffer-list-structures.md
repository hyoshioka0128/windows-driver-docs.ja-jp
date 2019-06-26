---
title: 派生 NET_BUFFER_LIST 構造
description: 派生 NET_BUFFER_LIST 構造
ms.assetid: 6660aef5-ba67-4f15-98b6-547fa753bc76
keywords:
- NET_BUFFER_LIST
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
- 構造体の派生 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410a584a46ac704fe6cd43c8ed7ccfc26417e689
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381458"
---
# <a name="derived-netbufferlist-structures"></a>NET の派生\_バッファー\_リストの構造体





NDIS ドライバーを使用して管理する機能を提供する[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の他の NET から派生した\_バッファー\_リストの構造体。 これらの関数は通常、中間ドライバーによって使用されます。

次の NDIS 関数が派生 NET を作成できます\_バッファー\_リスト構造既存の NET から\_バッファー\_リスト構造。

[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateclonenetbufferlist)

[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)

[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)

これらの関数では、NDIS は、ネットワーク データをコピーせず、派生の構造を作成するため、システム パフォーマンスが向上します。 3 つの種類があります[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)既存の NET から派生できる構造\_バッファー\_リスト構造。

<a href="" id="clone"></a>複製  
A 複製 NET\_バッファー\_リスト構造は、元のデータを参照する重複しています。 ドライバーは、構造体のこの型を使用して、複数のパスを同じデータを効率的に転送します。

<a href="" id="fragment"></a>フラグメント  
フラグメント[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体にはセットが含まれています[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)、元のデータを参照している構造体ただし、データは、最大サイズを超えないを単位に分割されます。 ドライバーは、大きなバッファー サイズより小さなバッファーを効率的に分割するこの種類の構造体を使用できます。

<a href="" id="reassembled"></a>再構築  
再構築された NET\_バッファー\_リスト構造体には、NET が含まれています\_NET の複数のソースから、元のデータを参照するバッファー構造\_バッファーの構造体。 ドライバーでは、この種類の構造体を使用して、1 つの大きなバッファーに多くの小さなバッファーを効率的に結合します。

この次のトピックの詳細情報派生 NET\_バッファー\_リストの構造体。

-   [NET 間のリレーションシップ\_バッファー\_一覧の世代](relationships-between-net-buffer-list-generations.md)
-   [NET の複製\_バッファー\_リストの構造体](cloned-net-buffer-list-structures.md)
-   [NET の断片化\_バッファー\_リストの構造体](fragmented-net-buffer-list-structures.md)
-   [NET の再構成\_バッファー\_リストの構造体](reassembled-net-buffer-list-structures.md)

 

 





