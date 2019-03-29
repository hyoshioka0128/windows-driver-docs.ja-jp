---
title: WDI_TLV_IPV6_LSO_V2 (0xD4)
description: WDI_TLV_IPV6_LSO_V2 では、IPv6 の大規模なオフロード V2 の送信パラメーターを含む TLV です。
ms.assetid: 898257D1-405A-46A3-AE63-26DFA8C1FAAC
ms.date: 07/18/2017
keywords:
- WDI_TLV_IPV6_LSO_V2 (0xD4) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bb7912d8cb30bd2c25ad53e8c6adb488e65f2e7b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580207"
---
# <a name="wditlvipv6lsov2-0xd4"></a>WDI\_TLV\_IPV6\_LSO\_V2 (0xD4)


WDI\_TLV\_IPV6\_LSO\_V2 は、IPv6 の大規模なオフロード V2 の送信パラメーターを含む TLV します。

記載されている機能の値が報告[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)します。 NDIS を使用して、\_オフロード\_いない\_サポートと NDIS\_オフロード\_を介して機能を指定する際にサポートされている[OID\_WDI\_GET\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)します。

## <a name="tlv-type"></a>TLV 型


0xD4

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
<tr class="even">
<td>UINT32</td>
<td>拡張機能の IP ヘッダーのあるパケットのチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>TCP オプションを使用してチェックサムのオフロードがサポートされているかどうかを指定します。</td>
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

 

 




