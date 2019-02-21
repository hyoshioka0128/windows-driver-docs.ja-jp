---
title: 派生 NET_BUFFER_LIST 構造体
description: 派生 NET_BUFFER_LIST 構造体
ms.assetid: 6660aef5-ba67-4f15-98b6-547fa753bc76
keywords:
- NET_BUFFER_LIST
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
- 構造体の派生 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22822826e647c5ba9e541eecfbc802a57c203dae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531130"
---
# <a name="derived-netbufferlist-structures"></a>NET の派生\_バッファー\_リストの構造体





NDIS ドライバーを使用して管理する機能を提供する[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の他の NET から派生した\_バッファー\_リストの構造体。 これらの関数は通常、中間ドライバーによって使用されます。

次の NDIS 関数が派生 NET を作成できます\_バッファー\_リスト構造既存の NET から\_バッファー\_リスト構造。

[**NdisAllocateCloneNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560705)

[**NdisAllocateFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560707)

[**NdisAllocateReassembledNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561614)

これらの関数では、NDIS は、ネットワーク データをコピーせず、派生の構造を作成するため、システム パフォーマンスが向上します。 3 つの種類があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)既存の NET から派生できる構造\_バッファー\_リスト構造。

<a href="" id="clone"></a>複製  
A 複製 NET\_バッファー\_リスト構造は、元のデータを参照する重複しています。 ドライバーは、構造体のこの型を使用して、複数のパスを同じデータを効率的に転送します。

<a href="" id="fragment"></a>フラグメント  
フラグメント[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体にはセットが含まれています[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)、元のデータを参照している構造体ただし、データは、最大サイズを超えないを単位に分割されます。 ドライバーは、大きなバッファー サイズより小さなバッファーを効率的に分割するこの種類の構造体を使用できます。

<a href="" id="reassembled"></a>再構築  
再構築された NET\_バッファー\_リスト構造体には、NET が含まれています\_NET の複数のソースから、元のデータを参照するバッファー構造\_バッファーの構造体。 ドライバーでは、この種類の構造体を使用して、1 つの大きなバッファーに多くの小さなバッファーを効率的に結合します。

この次のトピックの詳細情報派生 NET\_バッファー\_リストの構造体。

-   [NET 間のリレーションシップ\_バッファー\_一覧の世代](relationships-between-net-buffer-list-generations.md)
-   [NET の複製\_バッファー\_リストの構造体](cloned-net-buffer-list-structures.md)
-   [NET の断片化\_バッファー\_リストの構造体](fragmented-net-buffer-list-structures.md)
-   [NET の再構成\_バッファー\_リストの構造体](reassembled-net-buffer-list-structures.md)

 

 





