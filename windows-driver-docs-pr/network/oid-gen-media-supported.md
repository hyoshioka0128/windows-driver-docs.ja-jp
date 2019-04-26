---
title: OID_GEN_MEDIA_SUPPORTED
description: クエリとしては、OID_GEN_MEDIA_SUPPORTED OID は、NIC をサポートするメディアの種類が、必ずしも、NIC が現在使用しているメディアの種類を指定します。
ms.assetid: e7b8d2b1-4e84-416f-aeb3-75591ed44b22
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_SUPPORTED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6b121850c66dc8990be0701c6e5d5dd05d33ea0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348190"
---
# <a name="oidgenmediasupported"></a>OID\_GEN\_メディア\_サポートされています。


クエリ、OID として\_GEN\_メディア\_OID のサポートは、NIC をサポートするメディアの種類が、必ずしも、NIC が現在使用しているメディアの種類を指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
使われていません。

NDIS 6.0 とそれ以降のドライバーのメディアの種類が追加されました。

-   **NdisMediumTunnel**

-   **NdisMediumLoopback**

-   **NdisMediumNative802\_11**

NDIS 6.20 が動作し、以降のドライバーのメディアの種類が追加されました。

-   **NdisMediumIP**

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。 参照してください[OID\_GEN\_メディア\_(NDIS 5.1) サポートされている](https://msdn.microsoft.com/library/windows/hardware/ff560254)します。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。 参照してください[OID\_GEN\_メディア\_(NDIS 5.1) サポートされている](https://msdn.microsoft.com/library/windows/hardware/ff560254)します。

<a name="remarks"></a>コメント
-------

NDIS 6.0 とそれ以降のミニポート ドライバーでは、この OID 要求は表示されません。 NDIS は、ミニポート ドライバーが初期化中に指定するキャッシュされた値を持つこの OID を処理します。

これらのメディア タイプは、次のシステム定義の値の適切なサブセットとして表示されます。

<a href="" id="ndismedium802-3"></a>**NdisMedium802\_3**  
イーサネット (802.3)。

**注**  NDIS 5 *。x* 802.11 インターフェイスに準拠しているミニポート ドライバーは、このメディアの種類を使用する必要があります。 802.11 インターフェイスの詳細については、次を参照してください。 [802.11 ワイヤレス LAN のミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff543933)します。

 

<a href="" id="ndismedium802-5"></a>**NdisMedium802\_5**  
トークン リング (802.5)。 NDIS 6.0 およびそれ以降のドライバーは、このメディアの種類はサポートされていません。

**注**  以降 Windows 8 では、オペレーティング システムがサポートしていませんこのメディアの種類すべてのミニポート ドライバー。

 

<a href="" id="ndismediumfddi"></a>**NdisMediumFddi**  
FDDI します。 Windows Vista および Windows の以降のバージョンでは、このメディアの種類はサポートされていません。

<a href="" id="ndismediumwan"></a>**NdisMediumWan**  
WAN

<a href="" id="ndismediumlocaltalk"></a>**NdisMediumLocalTalk**  
LocalTalk

<a href="" id="ndismediumdix"></a>**NdisMediumDix**  
DEC/Intel/Xerox (DIX) イーサネット

<a href="" id="ndismediumarcnetraw"></a>**NdisMediumArcnetRaw**  
ARCNET (raw)。 Windows Vista および Windows の以降のバージョンでは、このメディアの種類はサポートされていません。

<a href="" id="ndismediumarcnet878-2"></a>**NdisMediumArcnet878\_2**  
ARCNET (878.2)。 Windows Vista および Windows の以降のバージョンでは、このメディアの種類はサポートされていません。

<a href="" id="ndismediumatm"></a>**NdisMediumAtm**  
ATM します。 NDIS 6.0 およびそれ以降のドライバーは、このメディアの種類はサポートされていません。

<a href="" id="ndismediumnative802-11"></a>**NdisMediumNative802\_11**  
ネイティブの 802.11 します。 このメディアの種類は、ネイティブの 802.11 インターフェイスに準拠しているミニポート ドライバーによって使用されます。 このインターフェイスの詳細については、次を参照してください。 [802.11 ワイヤレス LAN のネイティブのミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff560648)します。

<a href="" id="ndismediumwirelesswan"></a>**NdisMediumWirelessWan**  
さまざまな種類の **NdisWireless * * * Xxx*メディア。 このメディアの種類は、Windows Vista および Windows の以降のバージョン以降の使用をご利用いただけません。

<a href="" id="ndismediumirda"></a>**NdisMediumIrda**  
赤外線 (IrDA)。

<a href="" id="ndismediumcowan"></a>**NdisMediumCoWan**  
WAN の接続指向です。

<a href="" id="ndismedium1394"></a>**NdisMedium1394**  
IEEE 1394 (firewire) バスです。 Windows Vista および Windows の以降のバージョンでは、このメディアの種類はサポートされていません。

<a href="" id="ndismediumbpc"></a>**NdisMediumBpc**  
PC の network をブロードキャストします。

<a href="" id="ndismediuminfiniband"></a>**NdisMediumInfiniBand**  
InfiniBand ネットワーク。

<a href="" id="ndismediumtunnel"></a>**NdisMediumTunnel**  
トンネル ネットワーク。

<a href="" id="ndismediumloopback"></a>**NdisMediumLoopback**  
NDIS ループバック ネットワーク。

<a href="" id="ndismediumip"></a>**NdisMediumIP**  
Raw IP パケットを送受信することのできるジェネリック中です。

NDIS 5. *x*オペレーティング システムおよびイーサネットのパケットとして NDIS ワイヤレス LAN (WLAN) またはワイヤレスの WAN (WWAN) パケットをサポートするミニポート ドライバーが表示されます。 これらの NDIS ドライバーは、イーサネット ネットワークとして、WWAN または WLAN のネットワークのサポートを提供する必要があります。 このようなドライバーとその中の宣言**NdisMedium802\_3**およびイーサネットを上位レベルの NDIS ドライバーをエミュレートします。 このようなドライバーを宣言する必要がありますも[OID\_GEN\_物理\_MEDIUM](oid-gen-physical-medium.md)適切な物理メディアをサポートする.

詳細については、NDIS 5.X WLAN ミニポート ドライバーを参照してください[802.11 ワイヤレス LAN のミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff543933)します。

NDIS 6.0 とそれ以降のミニポート ドライバー WLAN メディアをサポートするオペレーティング システムおよび NDIS IEEE 802.11 パケットとして表示されるパケットを転送します。 これらの NDIS ドライバーは、ネイティブの 802.11 ミニポート ドライバーとして WLAN のネットワークのサポートを提供する必要があります。 このようなドライバーとその中の宣言**NdisMediumNative802\_11**します。

ネイティブの 802.11 ミニポート ドライバーの詳細については、次を参照してください。 [802.11 ワイヤレス LAN のネイティブのミニポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff560648)します。

基になるミニポート ドライバーに返された場合**NULL**このクエリで、実験用のメディアの種類を使用されるかどうか、ドライバーを示す必要がありますまたは受信操作を使用して、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数。 このような基になるミニポート ドライバーにバインドされている任意のプロトコルは、このようなすべての問題を受け取り、プロトコル ドライバーのフィルターを適用できませんは、受信操作で[OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md)します。

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


[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)

[OID\_GEN\_現在\_パケット\_フィルター](oid-gen-current-packet-filter.md)

[OID\_GEN\_物理\_中](oid-gen-physical-medium.md)

 

 




