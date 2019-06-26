---
title: プロトコル ドライバーのデータの受信
description: プロトコル ドライバーのデータの受信
ms.assetid: 758c6a86-6704-410b-ba13-bf589b1e330f
keywords:
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53bcdac651cbd2eddcd54977facfc7e1621e5ce7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373318"
---
# <a name="receiving-data-in-protocol-drivers"></a>プロトコル ドライバーのデータの受信





次の図は、基本的な受信操作で、プロトコル ドライバー、NDIS、およびドライバー スタック内の基になるドライバーが含まれます。

![基本的なを示す図は、プロトコル ドライバー、ndis、およびドライバー スタック内の基になるドライバーの操作を受信します。](images/protocolreceive.png)

NDIS 呼び出しプロトコル ドライバーの[ *ProtocolReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)を処理する関数が基になるドライバーからインジケーターを受信します。 NDIS 呼び出し*ProtocolReceiveNetBufferLists*受信を示す値の関数を呼び出して、基になるドライバーから (たとえば、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)) を受信したネットワーク データまたはループバック データを示します。

場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *ProtocolReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)プロトコル ドライバーの所有権を保持するが設定されている、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体にそれを呼び出すまで、 [ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)関数。 NDIS が設定されている場合、 **NDIS\_受信\_フラグ\_リソース**フラグは、プロトコルのドライバーを保持できません、 **NET\_バッファー\_一覧**構造と関連付けられているリソース。 セット**NDIS\_受信\_フラグ\_リソース**フラグは、基になるドライバーが不足していることを示しますでリソースを受信します。 ここで、 *ProtocolReceiveNetBufferLists*関数がプロトコルに割り当てられた記憶域に受信したデータをコピーし、可能な限り早くを返す必要があります。

**注**  NDIS は、基になるドライバーを示すフラグを変更できます。 たとえば、ミニポート ドライバーの設定、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*のパラメーター、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数、NDIS は指定されたデータをコピーしてへのコピーを渡す[ *ProtocolReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)で、**NDIS\_受信\_フラグ\_リソース**フラグをクリアします。

 

**注**  場合、 **NDIS\_受信\_フラグ\_リソース**フラグが設定されており、プロトコル ドライバーには、元のセットを保持する必要があります[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)リンク リスト内の構造体。 たとえば、このフラグが設定されている場合、ドライバー可能性があります、構造を処理、返しますが、元のリンクされたリストを復元する必要があります前に、一度に 1 つ、スタックにそれらを示します。

 

プロトコルのドライバーの呼び出し、 [ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)関数の一覧の所有権を解放する[ **NET\_バッファー\_ボックスの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の場合は、関連付けられていると共に、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体、およびネットワークのデータ。

 

 





