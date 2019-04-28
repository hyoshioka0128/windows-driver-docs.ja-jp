---
title: WDI_TLV_IPV4_LSO_V2 (0xD3)
description: WDI_TLV_IPV4_LSO_V2 では、IPv4 の大規模なオフロード V2 の送信パラメーターを含む TLV です。
ms.assetid: 912D5F1B-260F-43B3-93F6-3C38E9D7F1E5
ms.date: 07/18/2017
keywords:
- WDI_TLV_IPV4_LSO_V2 (0xD3) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 67ec713d8842231a1be77c7f3d2d7faa531e4064
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363024"
---
# <a name="wditlvipv4lsov2-0xd3"></a>WDI\_TLV\_IPV4\_LSO\_V2 (0xD3)


WDI\_TLV\_IPV4\_LSO\_V2 は、IPv4 の大規模なオフロード V2 の送信パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xD3

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>カプセル化の種類。 有効な値は次のとおりです。
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大サイズをオフロードします。 1 パケットあたり TCP ユーザー データのバイトの最大数で指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>セグメントの最小数。 セグメント化の後に存在する必要のあるセグメントの最小数で指定します。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




