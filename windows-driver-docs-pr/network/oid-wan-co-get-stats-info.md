---
title: OID_WAN_CO_GET_STATS_INFO
description: OID_WAN_CO_GET_STATS_INFO OID は、仮想接続 (VC) に固有である統計情報を返す、ミニポート ドライバーを要求します。
ms.assetid: 53ab1c04-7bb2-401d-ad54-72f3c1587dc0
ms.date: 08/08/2017
keywords: -OID_WAN_CO_GET_STATS_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7ae1e2597a80d8a917eca0616c23f19df5ee4eba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358736"
---
# <a name="oidwancogetstatsinfo"></a>OID\_WAN\_CO\_取得\_STATS\_情報


OID\_WAN\_CO\_取得\_STATS\_情報 OID (VC) の仮想接続に固有の統計情報を返す、ミニポート ドライバーを要求します。 統計情報を保持して、この OID、NDIS でのこれらの統計情報を返す、WAN ミニポート ドライバーが期待どおり\_WAN\_CO\_取得\_STATS\_情報構造体の次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_WAN_CO_GET_STATS_INFO {
         OUT ULONG BytesSent;
         OUT ULONG BytesRcvd;
         OUT ULONG FramesSent;
         OUT ULONG FramesRcvd;
         OUT ULONG CRCErrors;
         OUT ULONG TimeoutErrors;
         OUT ULONG AlignmentErrors;
         OUT ULONG SerialOverrunErrors;
         OUT ULONG FramingErrors;
         OUT ULONG BufferOverrunErrors;
         OUT ULONG BytesTransmittedUncompressed;
         OUT ULONG BytesReceivedUncompressed;
         OUT ULONG BytesTransmittedCompressed;
         OUT ULONG BytesReceivedCompressed;
    } NDIS_WAN_CO_GET_STATS_INFO,   *PNDIS_WAN_CO_GET_STATS_INFO;
```




この構造体のメンバーには、次の情報が含まれます。

<a href="" id="bytessent"></a>**BytesSent**  
送信バイト数を指定します。

<a href="" id="bytesrcvd"></a>**BytesRcvd**  
受信したバイト数を指定します。

<a href="" id="framessent"></a>**FramesSent**  
送信 (パケット WAN) のフレーム数を指定します。

<a href="" id="framesrcvd"></a>**FramesRcvd**  
受信したフレームの数を指定します。

<a href="" id="crcerrors"></a>**CRCErrors**  
この VC の CRC エラーの数を指定します。 CRC エラーは、巡回冗長検査の障害が原因です。 CRC エラーは、到着時に、正しく受信したフレーム内の 1 つまたは複数のバイトが検出されたことを示します。

<a href="" id="timeouterrors"></a>**TimeoutErrors**  
この VC で発生したタイムアウト エラーの数を指定します。 時間で、予期されたバイトを受信していない場合、タイムアウト エラーが発生します。

<a href="" id="alignmenterrors"></a>**AlignmentErrors**  
この VC の配置のエラーの数を指定します。 受信したバイトが予定のバイト数と異なる場合、配置エラーが発生します。 これは通常、バイト数が失われた場合、またはタイムアウト エラーが発生したときに発生します。

<a href="" id="serialoverrunerrors"></a>**SerialOverrunErrors**  
この VC で発生したシリアル オーバーランの数を指定します。 シリアル オーバーランは、WAN の NIC は、データの受信速度を処理できない場合に発生します。

<a href="" id="framingerrors"></a>**FramingErrors**  
この VC で発生したフレーム エラーの数を指定します。 無効な開始または停止ビットで非同期のバイトが受信したときに、フレーム エラーが発生します。

<a href="" id="bufferoverrunerrors"></a>**BufferOverrunErrors**  
この VC で発生したバッファー オーバーランの数を指定します。 WAN ミニポート ドライバーは、データの受信速度を処理できない場合、バッファー オーバーランが発生します。

<a href="" id="bytestransmitteduncompressed"></a>**BytesTransmittedUncompressed**  
送信される非圧縮データのバイト数を指定します。 ミニポート ドライバーは、圧縮をサポートしている場合にのみ、0 以外の値を返します。

<a href="" id="bytesreceiveduncompressed"></a>**BytesReceivedUncompressed**  
受信した圧縮されていないデータのバイト数を指定します。 ミニポート ドライバーは、圧縮をサポートしている場合にのみ、0 以外の値を返します。

<a href="" id="bytestransmittedcompressed"></a>**BytesTransmittedCompressed**  
送信される圧縮データのバイト数を指定します。 ミニポート ドライバーは、圧縮をサポートしている場合にのみ、0 以外の値を返します。

<a href="" id="bytesreceivedcompressed"></a>**BytesReceivedCompressed**  
受信した圧縮データのバイト数を指定します。 ミニポート ドライバーは、圧縮をサポートしている場合にのみ、0 以外の値を返します。

<a name="remarks"></a>注釈
-------

基になるドライバーまたはその NIC が圧縮をサポートしていない場合、ドライバーは、0 を返します、**バイト.非圧縮/圧縮**メンバー。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>








