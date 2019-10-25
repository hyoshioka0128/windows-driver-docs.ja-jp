---
title: NET_BUFFER 構造
description: NET_BUFFER 構造
ms.assetid: 6ba44aef-d4e6-4f18-8ae3-aebd8045791f
keywords:
- NET_BUFFER
- ネットワークデータ WDK, 構造
- データ WDK ネットワーク, 構造
- パケット WDK ネットワーク, データ構造
- NDIS_PACKET
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adcfdeebb383b96e91b4da880f2e3656fa114472
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829056"
---
# <a name="net_buffer-structure"></a>NET\_のバッファー構造





Ndis 6.0 以降の[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造は、ndis 5 で使用される[**ndis\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造に似ています。*x*以前のドライバー。 各 NET\_バッファー構造は、ネットワークデータのパケットをパッケージ化します。

次の図は、NET\_のバッファー構造内のフィールドを示しています。

![net\-のバッファー構造内のフィールドを示す図](images/netbuffer.png)

NET\_バッファー構造体には、 **NetBufferHeader**メンバーの[**net\_buffer\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_header)構造体が含まれています。 NET\_BUFFER\_HEADER 構造体には、 **NetBufferData**メンバーに[**net\_buffer\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)構造が含まれています。 NDIS マクロを使用して、NET\_バッファー構造体のメンバーにアクセスする必要があります。 これらのマクロの完全な一覧については、「 [**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造のリファレンス」ページを参照してください。

一部の[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体メンバーは、NDIS によってのみ使用されます。 ドライバーが通常使用するメンバーは次のとおりです。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
プロトコルドライバーで使用するために予約されています。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
ミニポートドライバーで使用するために予約されています。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
NET\_バッファー構造の割り当て元となる NET\_バッファープールを識別するプールハンドルを指定します。

<a href="" id="next"></a>**次に**  
NET\_BUFFER 構造体のリンクリスト内の次の NET\_BUFFER 構造体へのポインターを指定します。 この値がリスト内の最後の NET\_BUFFER 構造体である場合、このメンバーは**NULL**になります。

<a href="" id="datalength"></a>**DataLength**  
MDL チェーン内のネットワークデータの長さをバイト単位で指定します。

<a href="" id="dataoffset"></a>**DataOffset**  
Mdl チェーン内のメモリの先頭から、MDL チェーン内のネットワークデータの先頭までのオフセットをバイト単位で指定します。

<a href="" id="currentmdl"></a>**CurrentMdl**  
現在のドライバーが使用している最初の MDL へのポインターを指定します。 このポインターは、現在のドライバーが使用していない MDLs をスキップしてパフォーマンスを向上させる最適化を提供します。

<a href="" id="currentmdloffset"></a>**CurrentMdlOffset**  
NET\_BUFFER 構造体の**Currentmdl**メンバーによって指定された、MDL 内で使用されているデータ領域の先頭に対するオフセット (バイト単位) を指定します。

次の図は、 **Currentmdl**、 **currentmdloffset**、 **DataOffset**、および**DataLength**メンバーとデータ領域の関係を示しています。

![データ領域の割り当てを示す図](images/netbufferdata-wmdl.png)

NDIS には、MDL チェーン内のデータ領域を管理する関数が用意されています。 ドライバーが現在のドライバーを使用してデータ領域を動的に変更する方法。 現在のドライバーによって現在使用されていないデータ領域が存在する場合があります。 未使用の*データ領域*は現在使用されていませんが、有効なデータが含まれている場合があります。 たとえば、受信パスでは、下位レベルのドライバーによって使用されたヘッダー情報を、*未使用のデータ領域*に含めることができます。

ドライバーは、*使用されるデータ領域*を増減するために、retreat 操作と事前処理を実行します。 Retreat 操作と事前操作の詳細については、「 [Retreat 操作と事前操作](retreat-and-advance-operations.md)」を参照してください。

次の用語と定義では、 [**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)データ領域の要素について説明します。

<a href="" id="used-data-space"></a>使用済みデータ領域  
*使用中のデータ領域*現在のドライバーが現在の時刻に使用しているデータを格納します。 ドライバーは、*使用されているデータ領域*を引き上げ操作で増やし、*使用するデータ領域*を事前の操作で減らします。

<a href="" id="unused-data-space"></a>未使用のデータ領域  
現在のドライバーは、現在の時刻にこのデータ領域を使用していません。

<a href="" id="total-data-size"></a>合計データサイズ  
合計データサイズは、*使用さ*れているデータ領域と*未使用のデータ領域*のサイズの合計です。 合計サイズを計算するには、 **DataOffset**を**DataLength**に追加します。

<a href="" id="retreat"></a>戻り  
Retreat 操作は、*使用されるデータ領域*のサイズを増やします。

<a href="" id="advance"></a>切り替わる  
Advance 操作は、*使用されるデータ領域*のサイズを小さくします。

 

 





