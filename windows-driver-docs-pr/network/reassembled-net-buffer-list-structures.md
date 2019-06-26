---
title: 再構築された NET_BUFFER_LIST 構造
description: 再構築された NET_BUFFER_LIST 構造
ms.assetid: 0bfbfef3-c3ac-4add-b3b8-a4c3a96c8baa
keywords:
- NET_BUFFER_LIST
- WDK のネットワークを再構築された構造体
- 親/子 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- WDK NET_BUFFER_LIST のリレーションシップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e22aa219bf78e8ed928a29dad142073882ca6698
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368490"
---
# <a name="reassembled-netbufferlist-structures"></a>NET の再構成\_バッファー\_リストの構造体





再構築された NDIS ドライバーを作成できます[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)既存のネットから構造\_バッファー\_リスト構造体。 再構築された構造体は、複数のソースから、元のデータを参照[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。 ドライバーでは、この種類の構造体を使用して、1 つの大きなバッファーに多くの小さなバッファーを効率的に結合します。

次の図は、親 NET 間の関係を示します\_バッファー\_リスト構造と再構築された子構造体。

![net の親の間の関係を示す図\-バッファー\-構造および再構築された子構造体を一覧表示 ](images/netbufferlistreassembled.png)

上記の図には、親が含まれています。 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造とその親から派生した子構造体。 親の構造体が 1 つ[ **NET\_バッファー\_一覧\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造と 3 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) MDLs アタッチによる構造体。 親構造体の親ポインターが**NULL**派生構造ではないことを示します。

子 NET\_バッファー\_リスト構造が 1 つの NET\_アタッチ MDLs のバッファーの構造体。 子 NET\_バッファー\_リスト構造が親構造体へのポインター。 **NULL**場合、NET\_バッファー\_一覧\_コンテキスト構造体のポインターは、子に NET がないことを示しますなります\_バッファー\_一覧\_コンテキスト構造体。

NDIS ドライバー呼び出し、 [ **NdisAllocateReassembledNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)関数フラグメントの再構成に[ **NET\_バッファー\_ボックスの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 NDIS 割り当てる新しい[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造と再構築された net MDLs\_バッファー\_リスト構造体。 NDIS は、NET を割り当てません\_バッファー\_一覧\_再構築された構造体のコンテキスト構造体。 再構築された NET\_バッファーの構造と MDLs 親構造体と同じデータを記述します。 データはコピーされません。

再構築されたネットワークを作成する\_バッファー\_リスト構造、 **NdisAllocateReassembledNetBufferList**で指定されたバイトの数をスキップ、 *StartOffset*NET の親の各パラメーター\_バッファーの構造体。 **NdisAllocateReassembledNetBufferList** NET の各親の残りのデータを連結\_バッファーの構造体の 1 つの再構築された NET MDL チェーンに\_バッファーの構造体。 **NdisAllocateReassembledNetBufferList**研修 (使用されるデータ領域の増加) 再構築された NET\_バッファーの構造体で指定した量*DataOffsetDelta*します。

NDIS ドライバー呼び出し、 [ **NdisFreeReassembledNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreereassemblednetbufferlist)を再構築された解放関数[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造と関連付けられている[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造と MDL チェーン。

## <a name="related-topics"></a>関連トピック


[NET の派生\_バッファー\_リストの構造体](derived-net-buffer-list-structures.md)

 

 






