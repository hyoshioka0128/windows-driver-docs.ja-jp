---
title: OID_GEN_STATISTICS
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_STATISTICS OID を使用して、アダプターまたはミニポートドライバーの統計情報を取得します。
ms.assetid: ff81d6b0-806d-4ddf-9da1-a169221be61f
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_STATISTICS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: a09f3c297bab6e09b6b3cc1d595aecd8ab99dbab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844599"
---
# <a name="oid_gen_statistics"></a>OID\_GEN\_の統計情報


クエリとして、NDIS およびそれ以降のドライバーは、OID\_GEN\_STATISTICS OID を使用して、アダプターまたはミニポートドライバーの統計情報を取得します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
必ず.

NDIS\_STATISTICS\_INFO 構造体は、次のように定義されています。

```ManagedCPlusPlus
    typedef struct _NDIS_STATISTICS_INFO {
         NDIS_OBJECT_HEADER Header;
         ULONG SupportedStatistics;
         ULONG64 ifInDiscards;
         ULONG64 ifInErrors;
         ULONG64 ifHCInOctets;
         ULONG64 ifHCInUcastPkts;
         ULONG64 ifHCInMulticastPkts;
         ULONG64 ifHCInBroadcastPkts;
         ULONG64 ifHCOutOctets;
         ULONG64 ifHCOutUcastPkts;
         ULONG64 ifHCOutMulticastPkts;
         ULONG64 ifHCOutBroadcastPkts;
         ULONG64 ifOutErrors;
         ULONG64 ifOutDiscards;
         ULONG64 ifHCInUcastOctets;
         ULONG64 ifHCInMulticastOctets;
         ULONG64 ifHCInBroadcastOctets;
         ULONG64 ifHCOutUcastOctets;
         ULONG64 ifHCOutMulticastOctets;
         ULONG64 ifHCOutBroadcastOctets;
    } NDIS_STATISTICS_INFO, *PNDIS_STATISTICS_INFO;
```




この構造体には、次のメンバーが含まれます。

<a href="" id="header"></a>**項目**  
Ndis [ **\_オブジェクト\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) 、NDIS\_STATISTICS\_INFO 構造体のヘッダー構造です。 **ヘッダー**で\_指定されている構造体の**type**メンバーを、\_Type\_DEFAULT、 **REVISION**メンバーを NDIS\_STATISTICS\_INFO\_revision\_1、および Size に設定します。メンバーを NDIS\_SIZEOF\_統計\_情報\_リビジョン\_1 になります。

<a href="" id="supportedstatistics"></a>**SupportedStatistics**  
ミニポートドライバーがサポートする統計のセット。

**メモ** NDIS 6.0 以降のドライバーは、すべての統計をサポートしている必要があります。また、OID\_GEN\_統計を照会するときに、これらのドライバーを報告する必要があります



値は、次のフラグのビットごとの OR です。

<a href="" id="ndis-statistics-flags-valid-directed-frames-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効\_有向\_フレーム\_RCV  
**IfHCInUcastPkts**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効\_マルチキャスト\_フレーム\_RCV  
**IfHCInMulticastPkts**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効な\_ブロードキャスト\_フレーム\_RCV  
**IfHCInBroadcastPkts**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-bytes-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効な\_バイト\_RCV  
**IfHCInOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-rcv-discards"></a>NDIS\_STATISTICS\_フラグ\_有効な\_RCV\_破棄  
**IfInDiscards**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-rcv-error"></a>NDIS\_STATISTICS\_フラグ\_有効な\_RCV\_エラー  
**IfInErrors**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-directed-frames-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効\_有向\_フレーム\_XMIT  
**IfHCOutUcastPkts**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効\_マルチキャスト\_フレーム\_XMIT  
**IfHCOutMulticastPkts**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効\_ブロードキャスト\_フレーム\_XMIT  
**IfHCOutBroadcastPkts**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-bytes-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効な\_バイト\_XMIT  
**IfHCOutOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-xmit-error"></a>NDIS\_STATISTICS\_フラグ\_有効な\_XMIT\_エラー  
**IfOutErrors**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-xmit-discards"></a>NDIS\_STATISTICS\_フラグ\_有効な\_XMIT\_破棄  
**Ifoutdiscards**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効な\_転送\_バイト\_RCV  
**IfHCInUcastOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効な\_マルチキャスト\_バイト\_RCV  
**IfHCInMulticastOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-rcv"></a>NDIS\_STATISTICS\_フラグ\_有効な\_ブロードキャスト\_バイト\_RCV  
**IfHCInBroadcastOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効な\_転送\_バイト\_XMIT  
**IfHCOutUcastOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効\_マルチキャスト\_バイト\_XMIT  
**IfHCOutMulticastOctets**メンバーのデータは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-xmit"></a>NDIS\_STATISTICS\_フラグ\_有効な\_ブロードキャスト\_バイト\_XMIT  
**IfHCOutBroadcastOctets**メンバーのデータは有効です。

<a href="" id="ifindiscards"></a>**ifInDiscards**  
破棄された受信バッファーエラーの数。 これは、 [OID\_GEN\_RCV\_破棄](oid-gen-rcv-discards.md)によって返される値と同じです。

<a href="" id="ifinerrors"></a>**ifInErrors**  
受信エラー数。 このカウントは、 [OID\_GEN\_RCV\_ERROR](oid-gen-rcv-error.md)が返す値と同じです。

<a href="" id="ifhcinoctets"></a>**ifHCInOctets**  
受信方向のバイト数、受信マルチキャストのバイト数、および受信/ブロードキャストのバイト数の合計。 この合計は、 [OID\_GEN が\_バイト\_RCV](oid-gen-bytes-rcv.md)が返す値と同じです。

<a href="" id="ifhcinucastpkts"></a>**ifHCInUcastPkts**  
エラーを発生させずに受信したダイレクトパケットの数。 この数値は、 [OID\_GEN\_有\_フレーム\_RCV](oid-gen-directed-frames-rcv.md)が返す値と同じです。

<a href="" id="ifhcinmulticastpkts"></a>**ifHCInMulticastPkts**  
エラーを発生させずに受信したマルチキャスト/機能パケットの数。 この数値は、 [OID\_GEN\_マルチキャスト\_フレーム\_RCV](oid-gen-multicast-frames-rcv.md)が返す値と同じです。

<a href="" id="ifhcinbroadcastpkts"></a>**ifHCInBroadcastPkts**  
受信したブロードキャストパケットのうち、エラーが発生していないものの数。 この数値は、 [OID\_GEN\_ブロードキャスト\_フレーム\_RCV](oid-gen-broadcast-frames-rcv.md)が返す値と同じです。

<a href="" id="ifhcoutoctets"></a>**ifHCOutOctets**  
送信方向のバイト数、送信マルチキャストバイト数、および送信/ブロードキャストバイト数の合計。 この合計は、 [OID\_GEN\_バイト\_XMIT](oid-gen-bytes-xmit.md)が返す値と同じです。

<a href="" id="ifhcoutucastpkts"></a>**ifHCOutUcastPkts**  
エラーを発生させずに転送されるダイレクトパケットの数。 この数値は、 [OID\_GEN\_ダイレクトされる\_フレーム\_XMIT](oid-gen-directed-frames-xmit.md)が返す値と同じです。

<a href="" id="ifhcoutmulticastpkts"></a>**ifHCOutMulticastPkts**  
エラーが発生せずに転送されるマルチキャスト/機能パケットの数。 この数値は、 [OID\_GEN\_マルチキャスト\_フレーム\_XMIT](oid-gen-multicast-frames-xmit.md)が返す値と同じです。

<a href="" id="ifhcoutbroadcastpkts"></a>**ifHCOutBroadcastPkts**  
エラーが発生せずに転送されたブロードキャストパケットの数。 この数値は、 [OID\_GEN\_ブロードキャスト\_フレーム\_XMIT](oid-gen-broadcast-frames-xmit.md)が返す値と同じです。

<a href="" id="ifouterrors"></a>**ifOutErrors**  
送信エラーの数。 このカウントは、 [OID\_GEN\_XMIT\_ERROR](oid-gen-xmit-error.md)が返す値と同じです。

<a href="" id="ifoutdiscards"></a>**ifOutDiscards**  
インターフェイスによって破棄されたパケットの数。 これは、oid [\_GEN\_XMIT\_](oid-gen-xmit-discards.md)によって破棄された oid を照会することによって返される値と同じです。

<a href="" id="ifhcinucastoctets"></a>**ifHCInUcastOctets**  
受信パケットのバイト数。エラーが発生することはありません。 このカウントは、 [OID\_GEN\_](oid-gen-directed-bytes-rcv.md)指定された値と同じで、rcv が返す\_バイト\_ます。

<a href="" id="ifhcinmulticastoctets"></a>**ifHCInMulticastOctets**  
エラーを発生させずに受信したマルチキャスト/機能パケット内のバイト数。 このカウントは、 [OID\_GEN\_マルチキャスト\_バイト\_RCV](oid-gen-multicast-bytes-rcv.md)が返す値と同じです。

<a href="" id="ifhcinbroadcastoctets"></a>**ifHCInBroadcastOctets**  
受信したブロードキャストパケットのバイト数。エラーは発生しません。 このカウントは、 [OID\_GEN\_ブロードキャスト\_バイト\_RCV](oid-gen-broadcast-bytes-rcv.md)が返す値と同じです。

<a href="" id="ifhcoutucastoctets"></a>**ifHCOutUcastOctets**  
ダイレクトパケットのバイト数。エラーが発生することなく転送されます。 このカウントは、XMIT によって返される[\_バイト数\_\_の OID\_GEN](oid-gen-directed-bytes-xmit.md)と同じ値です。

<a href="" id="ifhcoutmulticastoctets"></a>**ifHCOutMulticastOctets**  
エラーが発生することなく転送されるマルチキャスト/機能パケット内のバイト数。 このカウントは、 [OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)が返す値と同じです。

<a href="" id="ifhcoutbroadcastoctets"></a>**ifHCOutBroadcastOctets**  
エラーが発生することなく転送されるブロードキャストパケット内のバイト数。 このカウントは、 [OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md)が返す値と同じです。

<a name="remarks"></a>注釈
-------

ミニポートドライバーは、統計カウンターを実装し、正しい統計値を報告する必要があります。 統計カウンターは、符号なし64ビット値です。 ミニポートドライバーは、NDIS\_統計\_情報構造の統計情報を返します。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[OID\_GEN\_ブロードキャスト\_バイト\_RCV](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_GEN\_ブロードキャスト\_フレーム\_RCV](oid-gen-broadcast-frames-rcv.md)

[OID\_GEN\_ブロードキャスト\_フレーム\_XMIT](oid-gen-broadcast-frames-xmit.md)

[OID\_GEN\_BYTES\_RCV](oid-gen-bytes-rcv.md)

[OID\_GEN\_BYTES\_XMIT](oid-gen-bytes-xmit.md)

[OID\_GEN\_ダイレクト\_バイト\_RCV](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_ダイレクト\_バイト\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_GEN\_ダイレクト\_フレーム\_RCV](oid-gen-directed-frames-rcv.md)

[OID\_GEN\_ダイレクト\_フレーム\_XMIT](oid-gen-directed-frames-xmit.md)

[OID\_GEN\_マルチキャスト\_フレーム\_RCV](oid-gen-multicast-frames-rcv.md)

[OID\_GEN\_マルチキャスト\_フレーム\_XMIT](oid-gen-multicast-frames-xmit.md)

[OID\_GEN\_マルチキャスト\_バイト\_RCV](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_GEN\_RCV\_破棄](oid-gen-rcv-discards.md)

[OID\_GEN\_RCV\_エラー](oid-gen-rcv-error.md)

[OID\_GEN\_XMIT\_破棄](oid-gen-xmit-discards.md)

[OID\_GEN\_XMIT\_エラー](oid-gen-xmit-error.md)








