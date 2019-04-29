---
title: OID_GEN_TRANSPORT_HEADER_OFFSET
description: セットとして OID_GEN_TRANSPORT_HEADER_OFFSET OID は、特定のトランスポートが送受信されるパケットの追加のヘッダーのサイズを示します。
ms.assetid: 00b00c5b-cdf3-4b87-8914-e87876c9ae23
ms.date: 08/08/2017
keywords: -OID_GEN_TRANSPORT_HEADER_OFFSET ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 56c52694a757b3eb5dbf37d4725e3151143603c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387889"
---
# <a name="oidgentransportheaderoffset"></a>OID\_GEN\_トランスポート\_ヘッダー\_オフセット


OID、セットとして\_GEN\_トランスポート\_ヘッダー\_OID のオフセットは、特定のトランスポートが送受信されるパケットの追加のヘッダーのサイズを示します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
任意。

<a name="remarks"></a>注釈
-------

トランスポートのミニポート ドライバーとこのヘッダーのサイズの複数層の他のドライバーに通知します。これらのドライバーのパケットを処理するときにこの情報を使用できます。 たとえば、ドライバーは; の IP ヘッダーの開始などのパケット内で上位レイヤー情報の先頭を検索するのに、トランスポートから取得した副層ヘッダーのサイズを使用できます。ドライバーは、でしたし、解析し、適切な IP プロトコル ヘッダーのフィールドを調整します。 トランスポートは、トランスポートを使用して\_ヘッダー\_をこのヘッダーのサイズを示すために、次のように定義されている、構造体のオフセットします。

```C++
typedef struct _TRANSPORT_HEADER_OFFSET {
  USHORT  ProtocolType; 
  USHORT  HeaderOffset; 
} TRANSPORT_HEADER_OFFSET, *PTRANSPORT_HEADER_OFFSET;
```

この構造体のメンバーには、次の情報が含まれます。

<a href="" id="protocoltype"></a>**プロトコルの種類**  
この OID を送信して、その後送信し、指定された副層ヘッダーのサイズを使用してパケットを受信するプロトコルの種類を指定します。 プロトコルでは、次の値の 1 つです。

<a href="" id="ndis-protocol-id-default"></a>NDIS\_プロトコル\_ID\_既定  
既定のプロトコル

<a href="" id="ndis-protocol-id-tcp-ip"></a>NDIS\_プロトコル\_ID\_TCP\_IP  
TCP/IP プロトコル

<a href="" id="ndis-protocol-id-ipx"></a>NDIS\_プロトコル\_ID\_IPX  
NetWare IPX プロトコル

<a href="" id="ndis-protocol-id-nbf"></a>NDIS\_プロトコル\_ID\_NBF  
NetBIOS プロトコル

<a href="" id="headeroffset"></a>**HeaderOffset**  
プロトコルをその後に送信またはミニポート ドライバーまたはその他の複数層のドライバーから受信したパケットのプロトコル ヘッダーの前にある副層ヘッダーのバイト単位のサイズを指定します。 たとえば、sizeof (イーサネット ヘッダー) + sizeof (スナップ ヘッダー)。

通常、トランスポートは、ミニポート ドライバーから取得した情報からパケットのヘッダーのサイズを計算します。 NIC をサポートするヘッダーを含むバイトのパケット サイズが使用を転送する最大の合計を要求する、 [OID\_GEN\_最大\_合計\_サイズ](oid-gen-maximum-total-size.md)OID。 NIC をサポートするバイトの最大パケット サイズを要求する、ヘッダーは含まれませんトランスポートで使用して、 [OID\_GEN\_最大\_フレーム\_サイズ](oid-gen-maximum-frame-size.md)OID。 ヘッダーの最大サイズを計算するには、トランスポートは、最大合計サイズの最大フレーム サイズを減算します。

トランスポートが副層ヘッダー情報を含むパケットを送信する場合、トランスポートこれらのパケットの副層ヘッダーのサイズを知る必要がありする必要があります基になるミニポート ドライバーやその他の階層型のドライバーについて通知サイズ、ドライバーが処理できるように、パケット。 パケット内で特定の副層ヘッダー情報を送受信する際に、特定のプロトコルのレジストリで設定できるオプションがある場合があります。 トランスポート副層ヘッダーに関する情報をレジストリから取得し、ミニポート ドライバーにヘッダーのサイズまたはその他の階層型のドライバーを渡します。

たとえば、トランスポートは、ファイバー分散データ インターフェイスの中からのパケットを処理する場合、トランスポートする必要がありますセットに要求を送信ミニポート ドライバーを基になると OID を使用して他の階層型ドライバー\_GEN\_トランスポート\_ヘッダー\_パケットの副層ヘッダーのサイズに関するこれらのドライバーを通知するためにオフセットします。 (FDDI は Windows Vista および Windows の以降のバージョンでないサポート)。FDDI からこれらのパケットには、論理リンク コントロール (LLC) 情報が含まれます。 この LLC の情報が、LLC ヘッダーとサブ ネットワーク アクセス プロトコル (スナップイン) などの他のヘッダーにさらに含まれます。 トランスポートは LLC/スナップインを使用する、レジストリから決定し、パケットの LLC/スナップイン セグメントのヘッダーのサイズをミニポート ドライバーに渡します。

この OID、ミニポート ドライバーではオプションと、その他の階層型ドライバー。 この OID は省略可能なため、ドライバーはこの OID を使用することが転送される要求に応答するために必要ありません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_GEN\_最大\_フレーム\_サイズ](oid-gen-maximum-frame-size.md)

[OID\_GEN\_最大\_合計\_サイズ](oid-gen-maximum-total-size.md)

 

 




