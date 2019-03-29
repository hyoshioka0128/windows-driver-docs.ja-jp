---
title: OID_GEN_STATISTICS
description: クエリとして NDIS および上にあるドライバーはアダプターのミニポート ドライバーの統計情報を取得するのに OID_GEN_STATISTICS OID を使用します。
ms.assetid: ff81d6b0-806d-4ddf-9da1-a169221be61f
ms.date: 08/08/2017
keywords: -OID_GEN_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cdf0225cb619a87db386adb6140a3472e80edfae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579305"
---
# <a name="oidgenstatistics"></a>OID\_GEN\_統計情報


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_統計 OID アダプターまたはミニポート ドライバーの統計情報を取得します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。

NDIS\_統計\_情報の構造は次のように定義されます。

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




この構造体には、次のメンバーが含まれています。

<a href="" id="header"></a>**ヘッダー**  
[ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588) NDIS 構造\_統計\_情報構造体。 設定、**型**、構造体のメンバーを**ヘッダー**を使用する NDIS\_オブジェクト\_型\_既定では、**リビジョン**NDIS にメンバー\_統計\_情報\_リビジョン\_1、および**サイズ**NDIS にメンバー\_SIZEOF\_統計\_情報\_リビジョン\_1。

<a href="" id="supportedstatistics"></a>**SupportedStatistics**  
ミニポート ドライバーがサポートする統計情報のセット。

**注**NDIS 6.0 とそれ以降のドライバーのすべての統計をサポートし、OID の照会されたときに報告する必要があります\_GEN\_統計。



値は、次のフラグのビットごとの OR です。

<a href="" id="ndis-statistics-flags-valid-directed-frames-rcv"></a>NDIS\_統計\_フラグ\_有効\_ダイレクト\_フレーム\_受信  
内のデータ、 **ifHCInUcastPkts**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-rcv"></a>NDIS\_統計\_フラグ\_有効\_マルチキャスト\_フレーム\_受信  
内のデータ、 **ifHCInMulticastPkts**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-rcv"></a>NDIS\_統計\_フラグ\_有効\_ブロードキャスト\_フレーム\_受信  
内のデータ、 **ifHCInBroadcastPkts**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-bytes-rcv"></a>NDIS\_統計\_フラグ\_有効\_バイト\_受信  
内のデータ、 **ifHCInOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-rcv-discards"></a>NDIS\_統計\_フラグ\_有効\_受信\_破棄  
内のデータ、 **ifInDiscards**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-rcv-error"></a>NDIS\_統計\_フラグ\_有効\_受信\_エラー  
内のデータ、 **ifInErrors**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-directed-frames-xmit"></a>NDIS\_統計\_フラグ\_有効\_ダイレクト\_フレーム\_XMIT  
内のデータ、 **ifHCOutUcastPkts**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-frames-xmit"></a>NDIS\_統計\_フラグ\_有効\_マルチキャスト\_フレーム\_XMIT  
内のデータ、 **ifHCOutMulticastPkts**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-frames-xmit"></a>NDIS\_統計\_フラグ\_有効\_ブロードキャスト\_フレーム\_XMIT  
内のデータ、 **ifHCOutBroadcastPkts**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-bytes-xmit"></a>NDIS\_統計\_フラグ\_有効\_バイト\_XMIT  
内のデータ、 **ifHCOutOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-xmit-error"></a>NDIS\_統計\_フラグ\_有効\_XMIT\_エラー  
内のデータ、 **ifOutErrors**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-xmit-discards"></a>NDIS\_統計\_フラグ\_有効\_XMIT\_破棄  
内のデータ、 **ifOutDiscards**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-rcv"></a>NDIS\_統計\_フラグ\_有効\_ダイレクト\_バイト\_受信  
内のデータ、 **ifHCInUcastOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-rcv"></a>NDIS\_統計\_フラグ\_有効\_マルチキャスト\_バイト\_受信  
内のデータ、 **ifHCInMulticastOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-rcv"></a>NDIS\_統計\_フラグ\_有効\_ブロードキャスト\_バイト\_受信  
内のデータ、 **ifHCInBroadcastOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-directed-bytes-xmit"></a>NDIS\_統計\_フラグ\_有効\_ダイレクト\_バイト\_XMIT  
内のデータ、 **ifHCOutUcastOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-multicast-bytes-xmit"></a>NDIS\_統計\_フラグ\_有効\_マルチキャスト\_バイト\_XMIT  
内のデータ、 **ifHCOutMulticastOctets**メンバーは有効です。

<a href="" id="ndis-statistics-flags-valid-broadcast-bytes-xmit"></a>NDIS\_統計\_フラグ\_有効\_ブロードキャスト\_バイト\_XMIT  
内のデータ、 **ifHCOutBroadcastOctets**メンバーは有効です。

<a href="" id="ifindiscards"></a>**ifInDiscards**  
削除-受信-バッファーのエラーの数。 これは、同じ値を[OID\_GEN\_受信\_破棄](oid-gen-rcv-discards.md)を返します。

<a href="" id="ifinerrors"></a>**ifInErrors**  
受信エラー数。 この数は同じ値を[OID\_GEN\_受信\_エラー](oid-gen-rcv-error.md)を返します。

<a href="" id="ifhcinoctets"></a>**ifHCInOctets**  
受信主導のバイト数、受信マルチキャスト バイト数、およびブロードキャストの受信バイト数の合計。 この合計は、同じ値を[OID\_GEN\_バイト\_受信](oid-gen-bytes-rcv.md)を返します。

<a href="" id="ifhcinucastpkts"></a>**ifHCInUcastPkts**  
エラーのない受信される有向のパケットの数。 この数は同じ値を[OID\_GEN\_ダイレクト\_フレーム\_受信](oid-gen-directed-frames-rcv.md)を返します。

<a href="" id="ifhcinmulticastpkts"></a>**ifHCInMulticastPkts**  
エラーのない受信したパケットがマルチキャスト/機能の数。 この数は同じ値を[OID\_GEN\_マルチキャスト\_フレーム\_受信](oid-gen-multicast-frames-rcv.md)を返します。

<a href="" id="ifhcinbroadcastpkts"></a>**ifHCInBroadcastPkts**  
エラーのない受信ブロードキャスト パケットの数。 この数は同じ値を[OID\_GEN\_ブロードキャスト\_フレーム\_受信](oid-gen-broadcast-frames-rcv.md)を返します。

<a href="" id="ifhcoutoctets"></a>**ifHCOutOctets**  
転送送信バイト数、送信マルチキャスト バイト数およびブロードキャスト送信バイト数の合計。 この合計は、同じ値を[OID\_GEN\_バイト\_XMIT](oid-gen-bytes-xmit.md)を返します。

<a href="" id="ifhcoutucastpkts"></a>**ifHCOutUcastPkts**  
エラーなしで送信される有向のパケットの数。 この数は同じ値を[OID\_GEN\_ダイレクト\_フレーム\_XMIT](oid-gen-directed-frames-xmit.md)を返します。

<a href="" id="ifhcoutmulticastpkts"></a>**ifHCOutMulticastPkts**  
エラーなしで送信されるパケットがマルチキャスト/機能の数。 この数は同じ値を[OID\_GEN\_マルチキャスト\_フレーム\_XMIT](oid-gen-multicast-frames-xmit.md)を返します。

<a href="" id="ifhcoutbroadcastpkts"></a>**ifHCOutBroadcastPkts**  
エラーなしで送信されるブロードキャスト パケットの数。 この数は同じ値を[OID\_GEN\_ブロードキャスト\_フレーム\_XMIT](oid-gen-broadcast-frames-xmit.md)を返します。

<a href="" id="ifouterrors"></a>**ifOutErrors**  
送信エラーの数。 この数は同じ値を[OID\_GEN\_XMIT\_エラー](oid-gen-xmit-error.md)を返します。

<a href="" id="ifoutdiscards"></a>**ifOutDiscards**  
インターフェイスによって破棄されたパケットの数。 これはクエリを実行して返される値と同じ、 [OID\_GEN\_XMIT\_破棄](oid-gen-xmit-discards.md)OID。

<a href="" id="ifhcinucastoctets"></a>**ifHCInUcastOctets**  
有向パケットのエラーのない受信したバイト数。 この数は同じ値を[OID\_GEN\_ダイレクト\_バイト\_受信](oid-gen-directed-bytes-rcv.md)を返します。

<a href="" id="ifhcinmulticastoctets"></a>**ifHCInMulticastOctets**  
マルチキャスト機能/パケットのエラーのない受信したバイト数。 この数は同じ値を[OID\_GEN\_マルチキャスト\_バイト\_受信](oid-gen-multicast-bytes-rcv.md)を返します。

<a href="" id="ifhcinbroadcastoctets"></a>**ifHCInBroadcastOctets**  
エラーのない受信ブロードキャスト パケットのバイト数。 この数は同じ値を[OID\_GEN\_ブロードキャスト\_バイト\_受信](oid-gen-broadcast-bytes-rcv.md)を返します。

<a href="" id="ifhcoutucastoctets"></a>**ifHCOutUcastOctets**  
エラーなしで送信される有向のパケットのバイト数。 この数は同じ値を[OID\_GEN\_ダイレクト\_バイト\_XMIT](oid-gen-directed-bytes-xmit.md)を返します。

<a href="" id="ifhcoutmulticastoctets"></a>**ifHCOutMulticastOctets**  
エラーなしで送信されるパケットがマルチキャスト/機能のバイト数。 この数は同じ値を[OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)を返します。

<a href="" id="ifhcoutbroadcastoctets"></a>**ifHCOutBroadcastOctets**  
ブロードキャスト パケットのエラーのない転送されるバイト数。 この数は同じ値を[OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md)を返します。

<a name="remarks"></a>コメント
-------

ミニポート ドライバーは、統計カウンターを実装し、正しい統計値をレポートする必要があります。 統計カウンターは、符号なし 64 ビット値です。 NDIS ミニポート ドライバーが統計を返します\_統計\_情報構造体。

<a name="requirements"></a>必要条件
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


[**NDIS\_オブジェクト\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff566588)

[OID\_GEN\_ブロードキャスト\_バイト\_受信](oid-gen-broadcast-bytes-rcv.md)

[OID\_GEN\_ブロードキャスト\_バイト\_XMIT](oid-gen-broadcast-bytes-xmit.md)

[OID\_GEN\_ブロードキャスト\_フレーム\_受信](oid-gen-broadcast-frames-rcv.md)

[OID\_GEN\_ブロードキャスト\_フレーム\_XMIT](oid-gen-broadcast-frames-xmit.md)

[OID\_GEN\_バイト\_受信](oid-gen-bytes-rcv.md)

[OID\_GEN\_バイト\_XMIT](oid-gen-bytes-xmit.md)

[OID\_GEN\_ダイレクト\_バイト\_受信](oid-gen-directed-bytes-rcv.md)

[OID\_GEN\_ダイレクト\_バイト\_XMIT](oid-gen-directed-bytes-xmit.md)

[OID\_GEN\_ダイレクト\_フレーム\_受信](oid-gen-directed-frames-rcv.md)

[OID\_GEN\_ダイレクト\_フレーム\_XMIT](oid-gen-directed-frames-xmit.md)

[OID\_GEN\_マルチキャスト\_フレーム\_受信](oid-gen-multicast-frames-rcv.md)

[OID\_GEN\_マルチキャスト\_フレーム\_XMIT](oid-gen-multicast-frames-xmit.md)

[OID\_GEN\_マルチキャスト\_バイト\_受信](oid-gen-multicast-bytes-rcv.md)

[OID\_GEN\_マルチキャスト\_バイト\_XMIT](oid-gen-multicast-bytes-xmit.md)

[OID\_GEN\_受信\_破棄](oid-gen-rcv-discards.md)

[OID\_GEN\_受信\_エラー](oid-gen-rcv-error.md)

[OID\_GEN\_XMIT\_破棄](oid-gen-xmit-discards.md)

[OID\_GEN\_XMIT\_エラー](oid-gen-xmit-error.md)








