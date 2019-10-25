---
title: プロトコル ドライバーのデータの受信
description: プロトコル ドライバーのデータの受信
ms.assetid: 758c6a86-6704-410b-ba13-bf589b1e330f
keywords:
- データを受信する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42267f671d4cd1f33eaad7a0eaed962c670d4cb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843469"
---
# <a name="receiving-data-in-protocol-drivers"></a>プロトコル ドライバーのデータの受信





次の図は、プロトコルドライバー、NDIS、およびドライバースタック内の基になるドライバーを含む基本的な受信操作を示しています。

![プロトコルドライバー、ndis、およびドライバースタック内の基になるドライバーを含む基本的な受信操作を示す図](images/protocolreceive.png)

NDIS は、プロトコルドライバーの[*ProtocolReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数を呼び出して、基になるドライバーからの受信の通知を処理します。 NDIS は、基になるドライバーが受信確認関数 ( [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)など) を呼び出して、受信したネットワークデータまたはループバックデータを示すことを示す*ProtocolReceiveNetBufferLists*を呼び出します。

[*ProtocolReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)の*receiveflags*パラメーターで **\_フラグ\_リソースフラグを受け取る NDIS\_** が設定されていない場合、プロトコルドライバーは[**NET\_バッファーの所有権を保持し\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)関数を呼び出すまで構造体をリストします。 Ndis が **\_FLAGS\_リソース**フラグを受け取るように ndis\_設定すると、プロトコルドライバーは**NET\_BUFFER\_LIST**構造と関連リソースを保持できません。 Set **NDIS\_receive\_FLAGS\_resources**フラグは、基になるドライバーで低受信リソースが実行されていることを示します。 この場合、 *ProtocolReceiveNetBufferLists*関数は、受信したデータをプロトコルによって割り当てられたストレージにコピーし、できるだけ早く返す必要があります。

**  NDIS**は、基になるドライバーが示すフラグを変更することができます。 たとえば、ミニポートドライバーが、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るように ndis\_設定した場合、ndis は、指定されたデータをコピーし、**NDIS\_RECEIVE\_FLAGS\_RESOURCES**フラグがクリアされた状態で、コピーを[*ProtocolReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)に渡します。

 

**注**  **NDIS\_\_フラグ\_リソース**フラグが設定されている場合、プロトコルドライバーは、リンクリストの元の[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を保持する必要があります。 たとえば、このフラグが設定されている場合、ドライバーは構造体を処理し、一度に1つずつスタックを示しますが、関数から制御が戻る前に、元のリンクリストを復元する必要があります。

 

プロトコルドライバーは、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)関数を呼び出して、関連付けられている[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造およびネットワークデータと共に、 [**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の一覧の所有権を解放します。

 

 





