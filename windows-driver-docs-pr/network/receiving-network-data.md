---
title: ネットワーク データの受信
description: ネットワーク データの受信
ms.assetid: d929c956-73dc-433f-9e60-bc3f8e0bcc14
keywords:
- ネットワークデータ WDK、受信
- データ WDK ネットワーク、受信
- パケット WDK ネットワーク、受信
- データを返す WDK ネットワーク
- ネットワークデータ WDK、返す
- データ WDK ネットワーク、返す
- パケット WDK ネットワーク、返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3250c3f41e4914a947f3bb7d221b05c15031ce8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844841"
---
# <a name="receiving-network-data"></a>ネットワーク データの受信





次の図は、ミニポートドライバー、NDIS、およびプロトコルドライバーを含む基本的な受信操作を示しています。

![基本的な受信操作を示す図](images/netbufferreceive.png)

ミニポートドライバーは、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出して、上位レベルのドライバーに対して[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を指定します。 各 NET\_バッファー構造体は、通常、別の[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体にアタッチする必要があります。 これにより、プロトコルドライバーは、元の一連の NET\_BUFFER\_リスト構造のサブセットを作成して、異なるクライアントに転送できます。 一部のドライバー (たとえば、ネイティブ IEEE 802.11 ミニポートドライバー) では、複数の NET\_バッファー構造を、NET\_バッファー\_の一覧構造にアタッチすることがあります。

すべての NET\_BUFFER\_LIST 構造体をリンクした後、ミニポートドライバーは、リスト内の最初の NET\_BUFFER\_LIST 構造体へのポインターを**NdisMIndicateReceiveNetBufferLists**関数に渡します。 NDIS は、NET\_BUFFER\_LIST 構造体を調べ、NET\_BUFFER\_リスト構造に関連付けられている各プロトコルドライバーの[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)関数を呼び出します。 NDIS は、各プロトコルドライバーへの適切なバインドに関連付けられている NET\_BUFFER\_LIST 構造のみを含むリストのサブセットを渡します。 NDIS は、NET\_BUFFER\_LIST 構造体で指定されている**NetBufferListFrameType**値を、各プロトコルドライバーが登録するフレームの種類に一致させることができます。

プロトコルドライバーの*ProtocolReceiveNetBufferLists*関数に渡される*receiveflags*パラメーターで\_フラグ\_リソースフラグを受け取る ndis\_が設定されている場合、ndis は NET の所有権を取り戻す[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) *ProtocolReceiveNetBufferLists*呼び出しが返された直後に、バッファー\_リスト構造体。

**注**  NDIS\_\_フラグ\_リソースフラグが設定されている場合、プロトコルドライバーは、リンクリストの元の NET\_BUFFER\_リスト構造を保持する必要があります。 たとえば、このフラグが設定されている場合、ドライバーは構造体を処理し、一度に1つずつスタックを示しますが、関数から制御が戻る前に、元のリンクリストを復元する必要があります。

 

プロトコルドライバーの*ProtocolReceiveNetBufferLists*関数に渡される*receiveflags*パラメーターで\_フラグ\_リソースフラグを受け取る NDIS\_が設定されていない場合、プロトコルドライバーは NET の所有権を保持することができます。\_バッファー\_リスト構造体。 この場合、プロトコルドライバーは、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)関数を呼び出すことによって、NET\_BUFFER\_LIST 構造体を返す必要があります。

ミニポートドライバーで受信リソースが不足している場合は、 **NdisMIndicateReceiveNetBufferLists**の呼び出しの*receiveflags*パラメーターで、NDIS\_RECEIVE\_FLAGS\_resources フラグを設定できます。 この場合、ドライバーは、 **NdisMIndicateReceiveNetBufferLists**がを返すとすぐに、指定されたすべての[**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造と埋め込みの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の所有権を再利用できます。 NDIS\_受信\_フラグ\_リソースフラグが設定された NET\_バッファー構造を指定すると、プロトコルドライバーによってデータが強制的にコピーされるため、回避する必要があります。 ミニポートドライバーは、受信リソースが不足していることを検出し、この状況を回避するために必要な手順を実行します。

NDIS は、プロトコルドライバーが**NdisReturnNetBufferLists**を呼び出すと、ミニポートドライバーの[*Miniportreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)関数を呼び出します。

  ミニポートドライバーによって、NDIS\_RECEIVE\_FLAGS\_RESOURCES フラグが設定された、\_バッファー\_のリスト構造が示されている場合には、NDIS が NET\_BUFFER\_LIST を示しているわけではないことに**注意**してください。同じ状態のプロトコルドライバーへの構造。 たとえば、NDIS は、NDIS\_RECEIVE\_FLAGS\_RESOURCES フラグを設定して、NET\_BUFFER\_LIST 構造体をコピーし、フラグがクリアされた状態でプロトコルドライバーへのコピーを示すことができます。

 

NDIS は、任意の順序で任意の組み合わせで、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をミニポートドライバーに返すことができます。 つまり、 *Miniportreturnnetbufferlists*関数の呼び出しによってミニポートドライバーに返される、NET\_BUFFER\_list 構造体のリンクリストは、前のさまざまな呼び出しからのネットワーク\_バッファー\_リスト構造を持つことができます。を**NdisMIndicateReceiveNetBufferLists**にします。

ミニポートドライバーでは、NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数のミニポートドライバーに提供する*miniportadapterhandle*に設定する必要があります。 フィルタードライバーは、フィルタードライバーが[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)のフィルタードライバーに提供したフィルターの**NdisFilterHandle**に由来する、各 NET\_BUFFER\_LIST 構造体の**sourcehandle**メンバーを設定する必要があります。プロシージャ. フィルタードライバーは、フィルタードライバーによって送信されていないすべての NET\_BUFFER\_リスト構造の**Sourcehandle**メンバーを変更することはできません。

また、中間ドライバーは、NET\_BUFFER\_LIST 構造体の**Sourcehandle**メンバーを、 *MiniportInitializeEx*関数の中間ドライバーに提供された*miniportadapterhandle*値に設定します。 中間ドライバーが受信通知を転送する場合、ドライバー**は sourcehandle メンバーに**書き込む前に、基になるドライバーが提供した**sourcehandle**値を保存する必要があります。 NDIS が転送された NET\_BUFFER\_LIST 構造体を中間ドライバーに返す場合、中間ドライバーは、保存した**Sourcehandle**を復元する必要があります。

 

 





