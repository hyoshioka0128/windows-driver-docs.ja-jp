---
title: 断片化された NET_BUFFER_LIST 構造体
description: 断片化された NET_BUFFER_LIST 構造体
ms.assetid: a72bc0cf-8c92-4c3e-ad10-710e5b93c74c
keywords:
- NET_BUFFER_LIST
- 断片化された構造の WDK ネットワーク
- データ構造の分割 WDK ネットワーク
- 親/子 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- リレーションシップ (WDK NET_BUFFER_LIST)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3fbd576c43675f9c04d2191b2858dae451fb698
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839645"
---
# <a name="fragmented-net_buffer_list-structures"></a>フラグメント化された NET\_BUFFER\_LIST 構造体





NDIS ドライバーでは、既存の NET\_BUFFER\_リスト構造から、フラグメント化された[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を作成できます。 断片化された構造体は、元のデータを参照する一連の[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体を参照します。ただし、データは最大サイズを超えない単位に分割されます。 ドライバーは、この種類の構造を使用して、大きなバッファーを効率的に小さなバッファーに分割できます。

次の図は、親の NET\_BUFFER\_LIST 構造体と、断片化された子との関係を示しています。

![親の net\-buffer\-list 構造体と、フラグメント化された子構造との関係を示す図](images/netbufferlistfragment.png)

上の図には、親の[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体と、その親から派生した子構造が含まれています。 親構造体には、1つの[**net\_バッファー\_リスト\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造、および mdls がアタッチされた1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造があります。 親の構造体の親ポインターが、派生構造ではないことを示す**NULL**です。

子の NET\_BUFFER\_LIST 構造体には、MDLs がアタッチされた3つの NET\_バッファー構造があります。 子の NET\_BUFFER\_LIST 構造体には、親の構造体へのポインターがあります。 **NULL**の場合、NET\_BUFFER\_LIST\_コンテキスト構造体ポインターは、子が NET\_BUFFER\_LIST\_context 構造体を持たないことを示します。

NDIS ドライバーは、 [**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)関数を呼び出して、既存の NET\_BUFFER\_リスト構造内のデータに基づいて、断片化された新しい[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を作成します。 NDIS は、フラグメント化された NET\_BUFFER\_LIST 構造体に新しい[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体と mdls を割り当てます。 NDIS は、フラグメント化された構造体の\_コンテキスト構造に、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)を割り当てません。 フラグメント NET\_のバッファー構造と MDLs は、親の構造と同じデータを記述します。 データはコピーされません。

**NdisAllocateFragmentNetBufferList**は、各親 NET\_バッファー構造内の*使用さ*れているデータ領域の先頭から開始し、 *StartOffset*パラメーターで指定された値までオフセットするフラグメントを作成します。

[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)は、各ソース NET\_バッファー構造内の*使用されているデータ領域*をフラグメントに分割します。 各フラグメントの使用されている*データ領域*の長さは、 *maximumlength*パラメーターで指定された値以下です。 最後のフラグメントの使用されている*データ領域*は、 *maximumlength*よりも小さくすることができます。 新しい NET\_バッファー構造のデータオフセットは、 *DataOffsetDelta*パラメーターに指定されたバイト数によって retreated されます。

親の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に複数の[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造がある場合 (図には示されていません)、各 net\_バッファー構造の断片化プロセスは、1つのデータ. たとえば、親の NET\_バッファー構造の最後のデータが最大サイズより小さい場合、NDIS は、次の NET\_バッファー構造の先頭にあるデータとこれらのデータを結合しません。

NDIS ドライバーは[**NdisFreeFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreefragmentnetbufferlist)関数を呼び出して[ **、net\_buffer\_LIST 構造体と、以前に割り当てられていたすべての関連する net\_buffer 構造体と MDL チェーンを解放します。NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)。

## <a name="related-topics"></a>関連トピック


[派生 NET\_BUFFER\_LIST 構造体](derived-net-buffer-list-structures.md)

 

 






