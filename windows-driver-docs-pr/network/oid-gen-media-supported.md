---
title: OID_GEN_MEDIA_SUPPORTED
description: クエリとして、OID_GEN_MEDIA_SUPPORTED OID は、NIC がサポートできるメディアの種類を指定しますが、NIC が現在使用しているメディアの種類は必ずしも使用しません。
ms.assetid: e7b8d2b1-4e84-416f-aeb3-75591ed44b22
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_MEDIA_SUPPORTED
ms.localizationpriority: medium
ms.openlocfilehash: 5a5f3f54eed66f8762b8e051a5d558f6486e2092
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843132"
---
# <a name="oid_gen_media_supported"></a>OID\_GEN\_メディア\_サポートされています


クエリとして、OID\_GEN\_メディア\_サポートされている OID は、NIC がサポートできるメディアの種類を指定しますが、NIC が現在使用しているメディアの種類は必ずしも使用できません。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
使われていません。

次のメディアの種類が NDIS 6.0 以降のドライバー用に追加されました。

-   **NdisMediumTunnel**

-   **NdisMediumLoopback**

-   **NdisMediumNative802\_11**

次のメディアの種類が NDIS 6.20 以降のドライバー用に追加されました。

-   **NdisMediumIP**

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず. [サポートされている OID\_GEN\_メディア\_サポート (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560254(v=vs.85))を参照してください。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
必ず. [サポートされている OID\_GEN\_メディア\_サポート (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560254(v=vs.85))を参照してください。

<a name="remarks"></a>注釈
-------

NDIS 6.0 以降のミニポートドライバーは、この OID 要求を受信しません。 NDIS は、この OID を、ミニポートドライバーが初期化時に提供するキャッシュされた値で処理します。

これらのメディアの種類は、システム定義の次の値の適切なサブセットとして一覧表示されます。

<a href="" id="ndismedium802-3"></a>**NdisMedium802\_3**  
イーサネット (802.3)。

  NDIS 5 に**注意**してください。802.11 インターフェイスに準拠している*x*ミニポートドライバーは、このメディアの種類を使用する必要があります。 802.11 インターフェイスの詳細については、「 [802.11 ワイヤレス LAN ミニポートドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff543933(v=vs.85))」を参照してください。

 

<a href="" id="ndismedium802-5"></a>**NdisMedium802\_5**  
トークンリング (802.5)。 このメディアの種類は、NDIS 6.0 以降のドライバーではサポートされていません。

**注**  Windows 8 以降では、オペレーティングシステムはミニポートドライバーにこのメディアの種類をサポートしていません。

 

<a href="" id="ndismediumfddi"></a>**NdisMediumFddi**  
FDDI. このメディアの種類は、Windows Vista 以降のバージョンの Windows ではサポートされていません。

<a href="" id="ndismediumwan"></a>**NdisMediumWan**  
WAN

<a href="" id="ndismediumlocaltalk"></a>**NdisMediumLocalTalk**  
LocalTalk

<a href="" id="ndismediumdix"></a>**NdisMediumDix**  
DEC/Intel/Xerox (DIX) イーサネット

<a href="" id="ndismediumarcnetraw"></a>**NdisMediumArcnetRaw**  
ARCNET (raw)。 このメディアの種類は、Windows Vista 以降のバージョンの Windows ではサポートされていません。

<a href="" id="ndismediumarcnet878-2"></a>**NdisMediumArcnet878\_2**  
ARCNET (878.2)。 このメディアの種類は、Windows Vista 以降のバージョンの Windows ではサポートされていません。

<a href="" id="ndismediumatm"></a>**NdisMediumAtm**  
ATM. このメディアの種類は、NDIS 6.0 以降のドライバーではサポートされていません。

<a href="" id="ndismediumnative802-11"></a>**NdisMediumNative802\_11**  
ネイティブ802.11。 このメディアの種類は、ネイティブ802.11 インターフェイスに準拠するミニポートドライバーによって使用されます。 このインターフェイスの詳細については、「[ネイティブ802.11 ワイヤレス LAN ミニポートドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff560648(v=vs.85))」を参照してください。

<a href="" id="ndismediumwirelesswan"></a>**NdisMediumWirelessWan**  
さまざまな種類の **NdisWireless * * * Xxx*メディア。 このメディアの種類は、Windows Vista 以降のバージョンの Windows 以降では使用できません。

<a href="" id="ndismediumirda"></a>**NdisMediumIrda**  
赤外線 (IrDA)。

<a href="" id="ndismediumcowan"></a>**NdisMediumCoWan**  
接続指向 WAN。

<a href="" id="ndismedium1394"></a>**NdisMedium1394**  
IEEE 1394 (firewire) バス。 このメディアの種類は、Windows Vista 以降のバージョンの Windows ではサポートされていません。

<a href="" id="ndismediumbpc"></a>**NdisMediumBpc**  
PC ネットワークをブロードキャストします。

<a href="" id="ndismediuminfiniband"></a>**NdisMediumInfiniBand**  
InfiniBand ネットワーク。

<a href="" id="ndismediumtunnel"></a>**NdisMediumTunnel**  
トンネルネットワーク。

<a href="" id="ndismediumloopback"></a>**NdisMediumLoopback**  
NDIS ループバックネットワーク。

<a href="" id="ndismediumip"></a>**NdisMediumIP**  
未加工の IP パケットを送受信できる汎用メディア。

NDIS 5。 ワイヤレス LAN (WLAN) またはワイヤレス WAN (WWAN) パケットをサポートする*x*ミニポートドライバーは、オペレーティングシステムと NDIS にイーサネットパケットとして表示されます。 これらの NDIS ドライバーは、イーサネットネットワークとしての WWAN または WLAN ネットワークのサポートを提供する必要があります。 このようなドライバーは、メディアを**NdisMedium802\_3**として宣言し、イーサネットを上位レベルの NDIS ドライバーにエミュレートします。 また、このようなドライバーでは、必要な物理メディアとして、[物理\_メディアを OID\_GEN\_](oid-gen-physical-medium.md)宣言する必要があります。「」をご利用ください。

NDIS 5. X WLAN ミニポートドライバーの詳細については、「 [802.11 ワイヤレス LAN ミニポートドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff543933(v=vs.85))」を参照してください。

NDIS 6.0 以降のミニポートドライバー。これは、オペレーティングシステムに表示され、NDIS に IEEE 802.11 パケットとして表示される WLAN メディア転送パケットをサポートします。 これらの NDIS ドライバーは、ネイティブ802.11 ミニポートドライバーとしての WLAN ネットワークのサポートを提供する必要があります。 このようなドライバーは、メディアを**NdisMediumNative802\_11**として宣言します。

ネイティブ802.11 ミニポートドライバーの詳細については、「[ネイティブ802.11 ワイヤレス LAN ミニポートドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff560648(v=vs.85))」を参照してください。

基になるミニポートドライバーがこのクエリに対して**NULL**を返した場合、または実験的なメディアの種類が使用されている場合、ドライバーは[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)関数を使用して受信操作を示す必要があります。 このような基になるミニポートドライバーにバインドされているすべてのプロトコルは、このようなすべての兆候を受け取ります。つまり、プロトコルドライバーでは、 [OID\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md)を使用して受信操作をフィルター処理することはできません。

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


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[OID\_GEN\_現在の\_パケット\_フィルター](oid-gen-current-packet-filter.md)

[OID\_GEN\_物理\_メディア](oid-gen-physical-medium.md)

 

 




