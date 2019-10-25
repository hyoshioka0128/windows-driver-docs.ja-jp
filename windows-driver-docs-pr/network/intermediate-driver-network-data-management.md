---
title: 中間ドライバー ネットワーク データ管理
description: 中間ドライバー ネットワーク データ管理
ms.assetid: 12f708b9-32f2-470c-bc4d-7c1b0c1012b1
keywords:
- 中間ドライバー WDK ネットワーク、ネットワークデータ管理
- NDIS 中間ドライバー WDK、ネットワークデータ管理
- ネットワークデータ管理 WDK NDIS 中間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e6159b9de085ee2e35304b8a08630b40499804
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844183"
---
# <a name="intermediate-driver-network-data-management"></a>中間ドライバー ネットワーク データ管理





中間ドライバーは、ネットワーク経由で送信するために、上位レベルのドライバーから1つ以上の関連する MDLs を使用して、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を受け取ります。 中間ドライバーは、ドライバーにコネクションレスエッジがある場合は[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)を呼び出し、ドライバーの接続指向が低い場合は[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)を呼び出すことによって、基になるドライバーにデータを渡すことができます。自動. また、中間ドライバーは、チェーンされたバッファーの内容、または受信データの順序やタイミングを他の転送と比較して変更する何らかのアクションを実行できます。

このようなドライバーでは、中間ドライバーの目的に応じて、着信する NET\_\_BUFFER にチェーンされているバッファーを再パッケージ化することができます。 たとえば、中間ドライバーは、次のような場合にネットワークデータを再パッケージ化します。

-   中間ドライバーは、基になるメディアで1つのバッファーに送信できるよりも、長いプロトコルドライバーから大きなデータバッファーを受け取ります。 そのため、中間ドライバーは、受信データをより小さなバッファーに分割する必要があります。

-   中間ドライバーは、各送信を基になるドライバーに転送する前にデータを圧縮または暗号化することによって、ネットワークデータの長さまたは内容を変更します。

ネットワークデータ管理の作成の詳細については、「[プロトコルドライバーのバッファー管理](protocol-driver-buffer-management.md)」を参照してください。

NDIS には、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を複製およびフラグメントするためのインターフェイスが用意されています。 構造体の複製と断片化の詳細については、「 [DERIVED NET\_BUFFER\_LIST 構造体](derived-net-buffer-list-structures.md)」を参照してください。

NET\_BUFFER\_LIST 構造体は、必要に応じて、ドライバーの初期化時、または[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数で割り当てることができます。 中間ドライバーの開発者は、必要に応じて、パフォーマンス上の理由から、初期化時にいくつかの構造体を割り当てて、 [**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)が、受信データをコピーするためのリソースを事前に割り当てられるようにします。上位レベルのドライバーに対して、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)が使用できるようになりました。これにより、1つ下のドライバーに着信送信ネットワークデータを渡すために、 [ **\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造 (および場合によってはバッファー) が使用\_できるようになります。

中間ドライバーが新しいバッファーにデータを送信するか、データを受信したときに、最後のバッファーの実際のデータの長さが、バッファーに割り当てられた長さよりも少ない場合、中間ドライバーは**NdisAdjustMdlLength**を呼び出してバッファーを調整できます。データの実際の長さ。

コネクションレスの下位エッジを持つ中間ドライバーは、常に、基になるミニポートアダプターからの受信データを[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数から受け取ります。

接続指向のエッジを持つ中間ドライバーは、常に、基になるミニポートアダプターからの受信データを[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)関数から受け取ります。

 

 





