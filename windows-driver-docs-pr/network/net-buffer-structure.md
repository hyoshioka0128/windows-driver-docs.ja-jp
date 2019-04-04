---
title: NET_BUFFER 構造体
description: NET_BUFFER 構造体
ms.assetid: 6ba44aef-d4e6-4f18-8ae3-aebd8045791f
keywords:
- NET_BUFFER
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
- NDIS_PACKET
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2339a151b20ca6196d0b669b69ae63b37ddea0f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552754"
---
# <a name="netbuffer-structure"></a>NET\_バッファーの構造体





NDIS 6.0 以降[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体に似ていますが、 [ **NDIS\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff557086)NDIS 5 を使用する構造体。*x*と以前のドライバーです。 各ネット\_バッファーの構造がネットワークのデータのパケットをパッケージ化します。

次の図は、NET でフィールドを示します\_バッファーの構造体。

![net のフィールドを示す図\-バッファーの構造](images/netbuffer.png)

NET\_バッファーの構造が含まれています、 [ **NET\_バッファー\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff568387)構造体、 **NetBufferHeader**メンバー。 NET\_バッファー\_ヘッダー構造が含まれています、 [ **NET\_バッファー\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568381)構造体、 **NetBufferData**メンバー。 NET のアクセスに NDIS マクロを使用する必要があります\_バッファー構造体のメンバー。 これらのマクロの完全な一覧を参照してください、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造のリファレンス ページです。

いくつかの[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体のメンバーは NDIS でのみ使用します。 ドライバーが通常使用されるメンバーは次のとおりです。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
プロトコル ドライバーで使用するために予約されています。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
ミニポート ドライバーで使用するために予約されています。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
NET を識別するプール ハンドルを指定します\_元のバッファー プール、NET\_割り当てられたバッファーの構造体。

<a href="" id="next"></a>**次に**  
[次へ] のネットワークへのポインターを指定します\_NET のリンク リストにバッファー構造\_バッファーの構造体。 この場合、最後の NET\_このメンバーの一覧で、バッファーの構造体が**NULL**します。

<a href="" id="datalength"></a>**DataLength**  
MDL チェーン内のネットワーク データのバイト単位の長さを指定します。

<a href="" id="dataoffset"></a>**DataOffset**  
メモリ MDL チェーン内のネットワーク データの先頭に MDL チェーン内の先頭からのバイト単位のオフセットを指定します。

<a href="" id="currentmdl"></a>**CurrentMdl**  
現在のドライバーを使用している最初の MDL へのポインターを指定します。 このポインターは、現在のドライバーを使用していない任意の MDLs をスキップしてパフォーマンスを向上する最適化を提供します。

<a href="" id="currentmdloffset"></a>**CurrentMdlOffset**  
オフセットをバイト単位で指定されている MDL で使用されるデータ領域の先頭を指定します、 **CurrentMdl** net メンバー\_バッファーの構造体。

次の図の間のリレーションシップを示しています、 **CurrentMdl**、 **CurrentMdlOffset**、 **DataOffset**、および**DataLength**メンバーは、データ領域。

![データ領域の割り当てを示す図](images/netbufferdata-wmdl.png)

NDIS は、MDL チェーン内のデータ領域を管理する機能を提供します。 ドライバーでのデータ領域の使用方法は、現在のドライバーを使用した動的に変更します。 現在のドライバーで現在使用されているデータ領域がある場合があります。 ただし、*未使用データ領域*現在使用されていない有効なデータを含めることができます。 たとえば、受信パス上、*未使用データ領域*下位レベルのドライバーで使用されたヘッダー情報を含めることができます。

ドライバーが撤退を実行し、進化を増減する操作、*使用データ領域*します。 撤退および高度な操作の詳細については、[撤退と高度な操作](retreat-and-advance-operations.md)を参照してください。

次の用語と定義の要素を記述、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)データ領域。

<a href="" id="used-data-space"></a>使用するデータ領域  
*使用中のデータ領域*現在のところ、現在のドライバーを使用しているデータが含まれています。 ドライバーを増やす*データ領域を使用*で退却操作し、削減*使用データ領域*高度な操作をします。

<a href="" id="unused-data-space"></a>未使用のデータ領域  
現在のドライバーは、このデータ領域を使用して、現在のところはいません。

<a href="" id="total-data-size"></a>合計データ サイズ  
合計データ サイズのサイズの合計です、*使用データ領域*と*未使用データ領域*します。 合計サイズを計算するには追加、 **DataOffset**を**DataLength**します。

<a href="" id="retreat"></a>撤退  
撤退操作のサイズを増やす、*使用データ領域*します。

<a href="" id="advance"></a>高度な  
高度な操作のサイズが小さく、*使用データ領域*します。

 

 





