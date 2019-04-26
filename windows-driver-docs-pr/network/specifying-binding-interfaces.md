---
title: バインド インターフェイスの指定
description: バインド インターフェイスの指定
ms.assetid: 49ef3eae-88e6-4424-8c3b-19e8c3bb734f
keywords:
- 追加レジストリ セクション WDK ネットワー キング、バインド インターフェイス
- WDK のネットワークをインターフェイスのバインド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b91c63325aaa4d929b277ef2871fa4f6c9d2085
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342584"
---
# <a name="specifying-binding-interfaces"></a>バインド インターフェイスの指定





インストールされる各ネットワーク コンポーネントのネットワーク INF ファイルは、追加することで、コンポーネントの上限と下限のバインド インターフェイスを指定する必要があります、**インターフェイス**キーを**Ndi**キー。

**インターフェイス**キーが少なくとも 2 つの値。

<a href="" id="upperrange"></a>**UpperRange**  
21\_SZ 値をコンポーネントが上端にバインドできるインターフェイスを定義します。

<a href="" id="lowerrange"></a>**LowerRange**  
21\_SZ 値をコンポーネントが下の端にバインドできるインターフェイスを定義します。 物理アダプターは、このインターフェイスは、イーサネット、アダプターが接続するなど、ネットワークのメディアは常にする必要があります。

**注**  、 **DefUpper**と**DefLower** Windows 95/98/ の値は、ただし、INF ファイルをネットワーク、Windows 2000 以降で使用される INF ファイルはサポートされていませんオペレーティング システムのバージョン。

 

次の表は、Microsoft が提供を一覧**UpperRange**値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>netbios</p></td>
<td align="left"><p>NetBIOS</p></td>
</tr>
<tr class="even">
<td align="left"><p>ipx</p></td>
<td align="left"><p>IPX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>tdi</p></td>
<td align="left"><p>TCP/IP に TDI インターフェイス</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5</p></td>
<td align="left"><p>NDIS 5.x (ndis2、ndis3、および ndis4 が使用できなく)。 上端で NDIS とやり取りする非 ATM アダプターなど、任意の非 ATM ネットワーク コンポーネントは、この値を指定する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndisatm</p></td>
<td align="left"><p>NDIS 5.x ATM をサポートします。 指定した値で NDIS 上端インターフェイスが、ATM アダプターなど、任意の ATM ネットワーク コンポーネント</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndiswan</p></td>
<td align="left"><p>WAN アダプターの上端。 指定した場合、この値が原因で RAS で使用するため、WAN アダプターを自動的に有効にするオペレーティング システム</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndiscowan</p></td>
<td align="left"><p>接続指向の NDIS を実行する WAN アダプターの上端</p></td>
</tr>
<tr class="even">
<td align="left"><p>noupper</p></td>
<td align="left"><p>上端バインディングの上端を公開しない任意のコンポーネントこのようなコンポーネントの通常、上端にあるプライベート インターフェイスであります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Winsock</p></td>
<td align="left"><p>Windows ソケット インターフェイス</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_atalk</p></td>
<td align="left"><p>上端 NDIS 5.x Net コンポーネント (アダプター) のみを上端に AppleTalk インターフェイスにバインドします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_dlc</p></td>
<td align="left"><p>上端 NDIS 5.x Net コンポーネント (アダプター) のみで、上端 DLC インターフェイスにバインドします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_ip</p></td>
<td align="left"><p>上端 NDIS 5.x Net コンポーネント (アダプター) のみ、上端に TCP/IP インターフェイスにバインドします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_ipx</p></td>
<td align="left"><p>上端 NDIS 5.x Net コンポーネント (アダプター) のみを上端に IPX インターフェイスにバインドします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_nbf</p></td>
<td align="left"><p>上端 NDIS 5.x Net コンポーネント (アダプター) のみで、上端 NetBEUI インターフェイスにバインドします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_streams</p></td>
<td align="left"><p>上端 NDIS 5.x Net コンポーネント (アダプター) のみで、上端のストリーム インターフェイスにバインドします。 この値は、Windows XP およびそれ以降のオペレーティング システムの廃止されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>flpp4</p></td>
<td align="left"><p>IPv4 をサポートしているモバイル ブロード バンド (MB) デバイス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>flpp6</p></td>
<td align="left"><p>IPv6 をサポートしているモバイル ブロード バンド (MB) デバイス。</p></td>
</tr>
</tbody>
</table>

 

次の表は、Microsoft が提供を一覧**LowerRange**値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>イーサネット</p></td>
<td align="left"><p>下端のイーサネット アダプター</p></td>
</tr>
<tr class="even">
<td align="left"><p>atm</p></td>
<td align="left"><p>ATM アダプターの下端</p></td>
</tr>
<tr class="odd">
<td align="left"><p>トークン リング</p></td>
<td align="left"><p>トークン リング アダプターの下端</p></td>
</tr>
<tr class="even">
<td align="left"><p>シリアル</p></td>
<td align="left"><p>下端シリアル アダプター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>fddi</p></td>
<td align="left"><p>FDDI アダプターの下端</p></td>
</tr>
<tr class="even">
<td align="left"><p>ベースバンド</p></td>
<td align="left"><p>下端ベースバンド アダプター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ブロード バンド</p></td>
<td align="left"><p>ブロード バンドのアダプターの下端</p></td>
</tr>
<tr class="even">
<td align="left"><p>Bluetooth</p></td>
<td align="left"><p>Bluetooth アダプターの下端</p></td>
</tr>
<tr class="odd">
<td align="left"><p>arcnet</p></td>
<td align="left"><p>下端 Arcnet アダプターの</p></td>
</tr>
<tr class="even">
<td align="left"><p>isdn</p></td>
<td align="left"><p>ISDN アダプターの下端</p></td>
</tr>
<tr class="odd">
<td align="left"><p>localtalk</p></td>
<td align="left"><p>下端 LocalTalk アダプター</p></td>
</tr>
<tr class="even">
<td align="left"><p>wan</p></td>
<td align="left"><p>下端 WAN アダプター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>nolower</p></td>
<td align="left"><p>下端バインディングの下端を公開しない任意のコンポーネント</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5</p></td>
<td align="left"><p>NDIS 5.x. (ndis2、ndis3、および ndis4 不要になった使用してください。)下端が NDIS を通じて非 ATM コンポーネントとインターフェイスのネットワーク コンポーネントの</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndisatm</p></td>
<td align="left"><p>Ndis 5.x ATM をサポートします。 任意のネットワーク コンポーネントの下端と連動する NDIS を通じて ATM コンポーネント</p></td>
</tr>
<tr class="even">
<td align="left"><p>wlan</p></td>
<td align="left"><p>802.11 ワイヤレス LAN のアダプターは、ネイティブの下端。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ppip</p></td>
<td align="left"><p>モバイル ブロード バンド (MB) アダプターの下端</p></td>
</tr>
<tr class="even">
<td align="left"><p>vwifi</p></td>
<td align="left"><p>下端仮想 wifi インターフェイス</p></td>
</tr>
</tbody>
</table>

 

**UpperRange**と**LowerRange**値では、--実際のコンポーネントとは - インターフェイスの種類を指定するコンポーネントをバインドできます。 バインディング エンジンは、ネットワーク コンポーネントを適切な (上限または下限) エッジで指定されたインターフェイスを提供するすべてのコンポーネントにバインドします。 プロトコルなど、 **LowerRange** ndis5 のバインドを持つすべてのコンポーネント、 **UpperRange** ndis5、物理または仮想アダプターなどの。

場合は、NDIS 5.x Net コンポーネント (アダプター) が 1 つまたは複数の特定のプロトコルでのみ動作し、その**UpperRange** ndis5 など、1 つまたは複数のプロトコルに応じた値を割り当てる必要があります\_atalk、ndis5\_dlc、ndis5\_ip、ndis5\_ipx、ndis5\_nbf、または ndis5\_ストリーム。 Net クラスのコンポーネントが割り当てられていない必要があります、 **UpperRange**値の ndis5、これが原因でそのコンポーネントにバインドするため、ndis5 を提供するすべてのプロトコルを下げるエッジ。

INF ファイル-ライターを定義し、ベンダー固有の使用**UpperRange**と**LowerRange**プライベート バインディング インターフェイスの値。 たとえば、ベンダー独自の専用プロトコル ドライバーにのみそのアダプターにバインドする場合は、INF ファイル ライター指定**XXX**の**UpperRange**アダプターのおよび**XXX**の**LowerRange**の専用プロトコルです。 Windows 2000 バインディング エンジンは、バインドを持つすべてのコンポーネント、 **UpperRange**の**XXX** (この場合は、アダプター) を持つすべてのコンポーネントと、 **LowerRange**の**XXX** (この例では、独自のプロトコル) では。

例を次に、*追加レジストリ セクション*を追加する**UpperRange**と**LowerRange** ATM アダプターの値。

```INF
[addreg-section]
HKR, Ndi\Interfaces, UpperRange, 0, "ndisATM"
HKR, Ndi\Interfaces, LowerRange, 0, "atm"
```

 

 





