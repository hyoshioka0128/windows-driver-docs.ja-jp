---
title: MB ミニポート ドライバーの INF の要件
description: MB ミニポート ドライバーの INF の要件
ms.assetid: 1f248e1c-7faf-4a11-a4c2-3c0e829e1583
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bbef3c703f47c2b0859b730613cd5451278bd65
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464336"
---
# <a name="mb-miniport-driver-inf-requirements"></a>MB ミニポート ドライバーの INF の要件


MB のミニポート ドライバーの INF ファイルで、次のエントリがあります。

```INF
*IfType  = 243; IF_TYPE_WWANPP 
*MediaType  = 9; <mark type="enumval">NdisMediumWirelessWan</mark> 
*PhysicalMediaType  = 8; NdisPhysicalMediumWirelessWan
EnableDhcp  = 0; Disable DHCP

;Entries to be put in add-registry-section for NdisMediumWirelessWan
HKR, Ndi\Interfaces, UpperRange, 0, "flpp4, flpp6"
HKR, Ndi\Interfaces, LowerRange, 0, "ppip"
```

AddReg と CopyFiles などのキーワードの場合と同じ INF セクション UpperRange と LowerRange を除く、上記のコード例で説明されているすべてのエントリがあります。 UpperRange と LowerRange 含める必要があります、[追加レジストリ セクション](add-registry-sections-in-a-network-inf-file.md)の INF ファイル。

### <a href="" id="-iftype"></a>\*IfType

デュアル モードのデバイスは、のいずれかを指定できます、 *IfType*次の表からの値。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>[説明]</strong></p></td>
<td align="left"><p><strong>名前</strong></p></td>
<td align="left"><p><strong>IfType</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>MB デバイスの GSM ベース</p></td>
<td align="left"><p>IF_TYPE_WWANPP</p></td>
<td align="left"><p>243</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MB デバイスの CDMA ベース</p></td>
<td align="left"><p>IF_TYPE_WWANPP2</p></td>
<td align="left"><p>244</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="-mediatype"></a>\*メディアの種類

MB のミニポート ドライバーでは、ミニポート ドライバーがその送信で解釈できると、データ パスの受信パケットのフレーミングの種類に基づいて、次の表からメディアの種類の値のいずれかを指定する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>[説明]</strong></p></td>
<td align="left"><p><strong>名前</strong></p></td>
<td align="left"><p><strong>メディアの種類</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>802.3 パケットを解釈する MB ミニポート ドライバーには、このメディアの種類を報告する必要があります。 このフレームワークは古いミニポート ドライバーの移行に対してのみ、運用品質のミニポート ドライバーはお勧めしません。</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>生 IP トラフィックを処理することができる MB ミニポート ドライバーでは、このメディアの種類を設定する必要があります。 これは、実稼働品質のミニポート ドライバーで使用することをお勧めのメディアの種類です。</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>9</p></td>
</tr>
</tbody>
</table>

 

### <a name="enabledhcp"></a>EnableDhcp

MB のミニポート ドライバーには、DHCP サーバーのエミュレーションを実装するかどうかに基づいて、次の表から EnableDhcp 値のいずれかを指定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>値</strong></p></td>
<td align="left"><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>このインターフェイスの DHCP を無効にします。 ミニポート ドライバーは、DHCP サーバーのなりすましを実装していません。 これは、実稼働品質のドライバーで使用される推奨値です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>このインターフェイスの DHCP を有効にします。 ミニポート ドライバーでは、DHCP サーバーのなりすましを実装します。 つまり、ミニポート ドライバーは、DHCP サーバーと ARP 解決策を偽装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="upperrange"></a>UpperRange

このキーワードは、メディアの種類が NdisMediumWirelessWan ときに、該当する場合は、次の文字列の 1 つまたは複数の組み合わせに設定されます。 NdisMedium802\_3 のミニポート ドライバーが UpperRange で既存の値を使用する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>値</strong></p></td>
<td align="left"><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>"flpp4"</p></td>
<td align="left"><p>MB デバイスは IPv4 をサポートしている場合、ミニポート ドライバーは"flpp4"を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"flpp6"</p></td>
<td align="left"><p>MB デバイスが IPv6 をサポートしている場合、ミニポート ドライバーは"flpp6"を指定します。 この値は、IPv6 をサポートするデバイスにのみ必要です。</p></td>
</tr>
</tbody>
</table>

 

### <a name="lowerrange"></a>LowerRange

このキーワードが必要で、少なくとも、メディアの種類が NdisMediumWirelessWan 時に、次の値です。 NdisMedium802\_3 のミニポート ドライバーが LowerRange で既存の値を使用する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>値</strong></p></td>
<td align="left"><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>"ppip"</p></td>
<td align="left"><p>下端の MB デバイスの種類。</p></td>
</tr>
</tbody>
</table>

 

 

 





