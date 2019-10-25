---
title: 派生 NET_BUFFER_LIST 構造体
description: 派生 NET_BUFFER_LIST 構造体
ms.assetid: 6660aef5-ba67-4f15-98b6-547fa753bc76
keywords:
- NET_BUFFER_LIST
- ネットワークデータ WDK, 構造
- データ WDK ネットワーク, 構造
- パケット WDK ネットワーク, データ構造
- 派生構造の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d970c35850e435335985f00b722b8af2650b072
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838157"
---
# <a name="derived-net_buffer_list-structures"></a>派生 NET\_BUFFER\_LIST 構造体





NDIS に用意されている関数を使用すると、ドライバーは、他の NET\_BUFFER\_リスト構造から派生した\_リスト構造体を使用して、 [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)を管理できます。 これらの関数は、通常、中間ドライバーによって使用されます。

次の NDIS 関数を使用すると、既存の NET\_BUFFER\_LIST 構造体から、派生した NET\_BUFFER\_LIST 構造体を作成できます。

[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateclonenetbufferlist)

[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)

[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)

NDIS はネットワークデータをコピーせずに派生構造を作成するため、これらの関数はシステムパフォーマンスを向上させます。 既存の NET\_BUFFER\_LIST 構造から派生できる、3種類の[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体があります。

<a href="" id="clone"></a>Clone  
複製された NET\_BUFFER\_LIST 構造体は、元のデータを参照する複製です。 ドライバーは、この種類の構造を使用して、同じデータを複数のパスに効率的に転送できます。

<a href="" id="fragment"></a>抜粋  
フラグメント[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体には、元のデータを参照する一連の[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体が含まれています。ただし、データは最大サイズを超えない単位に分割されます。 ドライバーは、この種類の構造を使用して、大きなバッファーを効率的に小さなバッファーに分割できます。

<a href="" id="reassembled"></a>再構築  
再構築された NET\_BUFFER\_LIST 構造体には、複数のソース NET\_バッファー構造の元のデータを参照する NET\_バッファー構造体が含まれています。 ドライバーは、この種類の構造を使用して、多数の小さいバッファーを効率的に1つの大きなバッファーに結合できます。

次のトピックでは、派生した NET\_BUFFER\_LIST 構造体の詳細について説明します。

-   [NET\_BUFFER\_LIST Generation のリレーションシップ](relationships-between-net-buffer-list-generations.md)
-   [複製された NET\_BUFFER\_LIST 構造体](cloned-net-buffer-list-structures.md)
-   [フラグメント化された NET\_BUFFER\_LIST 構造体](fragmented-net-buffer-list-structures.md)
-   [再構築した NET\_BUFFER\_LIST 構造体](reassembled-net-buffer-list-structures.md)

 

 





