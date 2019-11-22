---
title: フィルター ドライバーのデータの受信
description: フィルター ドライバーのデータの受信
ms.assetid: 4f6d44e9-c351-452d-aadf-505e6bb30fc2
keywords:
- データを受信する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcf5331eccfce91633f5fe4c73b84e4caf3ddb04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844856"
---
# <a name="receiving-data-in-a-filter-driver"></a>フィルター ドライバーのデータの受信





フィルタードライバーは、基になるドライバーから受信の表示を開始したり、受信の通知をフィルター処理したりできます。 ミニポートドライバーが[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を呼び出すと、NDIS は、指定された[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をドライバースタック内の最下位のフィルターモジュールに送信します。

### <a name="receive-indications-initiated-by-a-filter-driver"></a>フィルタードライバーによって開始される受信通知

次の図は、フィルタードライバーによって開始される受信通知を示しています。

![フィルタードライバーによって開始される受信通知を示す図](images/filterreceive.png)

フィルタードライバーは、受信したデータを示すために[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)関数を呼び出します。 **NdisFIndicateReceiveNetBufferLists**関数は、指定された一連の[**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を、スタックの上位のドライバーに渡します。 フィルタードライバーは、初期化中に作成されたプールから構造体を割り当てます。

フィルタードライバーが、 [**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るように NDIS\_設定した場合、フィルタードライバーは、[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をすぐに表示します。 この場合、NDIS は、フィルタードライバーの[*Filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数を呼び出して、 **NET\_BUFFER\_LIST**構造体を返しません。 フィルタードライバーは、 **NdisFIndicateReceiveNetBufferLists**が戻った直後に所有権を取得します。

フィルタードライバーによって、 **ndis\_RECEIVE flags パラメーターの\_FLAGS\_RESOURCES**フラグが設定されていない[**場合、ndis は、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)指定された[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体をフィルタードライバーの[*filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数に返します。 この場合、フィルタードライバーは、NDIS が*Filterreturnnetbufferlists*に戻るまで、指定された構造体の所有権を放棄します。

フィルタードライバーは、開始された受信通知を追跡し、受信操作が完了したときに[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)関数を呼び出さないようにする必要がある  **ことに注意**してください。

 

### <a name="filtering-receive-indications"></a>受信表示のフィルター処理

次の図は、基になるドライバーによって開始されるフィルター処理された受信通知を示しています。

![基になるドライバーによって開始されるフィルター処理された受信通知を示す図](images/receivefilter.png)

NDIS は、フィルタードライバーの[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)関数を呼び出して、基になるドライバーからの受信通知を処理します。 NDIS は、基になるドライバーが受信したネットワークデータやループバックデータを示す受信確認関数 ( [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)など) を呼び出すと、 *FilterReceiveNetBufferLists*を呼び出します。

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)の*receiveflags*パラメーターで **\_フラグ\_リソースフラグを受け取る NDIS\_** が設定されていない場合、フィルタードライバーは[**NET\_BUFFER\_LIST の所有権を保持します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)関数を呼び出すまでの構造体。

*Receiveflags*パラメーターで **\_FLAGS\_RESOURCES フラグを受け取る NDIS\_** が設定されている場合、フィルタードライバーは[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体と、関連付けられている基になるを保持できません。ドライバーによって割り当てられたリソース。 このフラグは、基になるドライバーが、受信リソースが不足していることを示している可能性があります。 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)関数は、できるだけ早くを返す必要があります。

**注**  **NDIS\_\_フラグ\_リソース**フラグが設定されている場合、フィルタードライバーは、リンクリストの元の[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造を保持する必要があります。 たとえば、このフラグが設定されている場合、ドライバーは構造体を処理し、一度に1つずつスタックを示しますが、関数が戻る前に、元のリンクリストを復元する必要があります。

 

フィルタードライバーは、受信したデータに対してフィルター操作を実行してから、そのドライバーにデータを通知することができます。 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)関数に送信された各バッファーに対して、フィルタードライバーは次の操作を実行できます。

-   [**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)を呼び出して、次に進むドライバーに渡します。 ドライバーは、バッファーの内容を変更できます。 NDIS では、コンテキスト空間の可用性が保証されます (「 [NET\_BUFFER\_LIST\_context structure](net-buffer-list-context-structure.md))」を参照してください。

    フィルタードライバーは、NDIS によって[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)に渡された状態を変更することも、単に[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)に渡すこともできます。

    [**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)を使用して、フィルタードライバーが[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)の*receiveflags*パラメーターに **\_\_\_ndis**を設定している場合でも、を使用し**てバッファーに**渡すことができます。   この場合、フィルタードライバーは、バッファーの所有権を取り戻すまで*FilterReceiveNetBufferLists*から戻らないようにする必要があります。

     

-   バッファーを破棄します。 Ndis によって\_Ndis がクリアされた場合は、 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るようにして、 [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)関数を呼び出してバッファーを破棄します。 NDIS で\_、FilterReceiveNetBufferLists の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るように ndis に設定した場合は、no action を実行し、バッファーを破棄するために*FilterReceiveNetBufferLists*からを返します。

-   後で処理するために、ローカルデータ構造でバッファーをキューに格納します。 NDIS で、 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)の*receiveflags*パラメーターに **\_FLAGS\_RESOURCES**フラグを受け取るように ndis\_設定した場合、フィルタードライバーは*FilterReceiveNetBufferLists*から戻る前にコピーを作成する必要があります。

-   バッファーをコピーし、そのコピーを使用して受信通知を開始します。 受信通知は、フィルタードライバーによって開始される受信通知に似ています。 この場合、ドライバーは元のバッファーを基になるドライバーに返す必要があります。

[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)関数は、指定された一連の[**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を、ドライバースタックを前のドライバーに渡します。 受信操作は、フィルタードライバーによって開始される受信操作と同様に処理されます。

それまでのドライバーがバッファーの所有権を保持している場合、NDIS はフィルターモジュールの[*Filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数を呼び出します。 *Filterreturnnetbufferlists*関数では、フィルタードライバーは、受信表示パスでバッファーに対して実行した操作を元に戻します。

最も低いレイヤーフィルターモジュールが、バッファーを使用して実行されたことを示している場合、NDIS はミニポートドライバーにバッファーを返します。 Ndis によって\_Ndis がクリアされた場合、 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取ると、フィルタードライバーは[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)を呼び出して、格納. NDIS で、 *FilterReceiveNetBufferLists*の*receiveflags*パラメーターで **\_FLAGS\_RESOURCES**フラグを受け取るように ndis\_受信した場合、 *FilterReceiveNetBufferLists*から戻ると、バッファーが返されます。

 

 





