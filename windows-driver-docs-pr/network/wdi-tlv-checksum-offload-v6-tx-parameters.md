---
title: WDI_TLV_CHECKSUM_OFFLOAD_V6_TX_PARAMETERS (0xDC)
description: WDI_TLV_CHECKSUM_OFFLOAD_V6_TX_PARAMETERS では、IPv6 のチェックサムがオフロード Tx を含む TLV です。
ms.assetid: F0340707-4E81-4E66-AF0E-A2918F4F5C7A
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_V6_TX_PARAMETERS (0xDC) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a9d6155ad7cc287e43288a5d79b66ceef8272945
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559430"
---
# <a name="wditlvchecksumoffloadv6txparameters-0xdc"></a>WDI\_TLV\_チェックサム\_オフロード\_V6\_TX\_パラメーター (0xDC)


WDI\_TLV\_チェックサム\_オフロード\_V6\_TX\_パラメーターは、IPv6 の Tx チェックサム オフロード用を含む TLV します。

記載されている機能の値が報告[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)します。 NDIS を使用して、\_オフロード\_いない\_サポートと NDIS\_オフロード\_を介して機能を指定する際にサポートされている[OID\_WDI\_GET\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)します。

## <a name="tlv-type"></a>TLV 型


0xDC

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
<th>種類</th>
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
<td>拡張機能の IP ヘッダーのあるパケットのチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>TCP オプションを使用してチェックサムのオフロードがサポートされているかどうかを指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>TCP チェックサム オフロードが有効になっているかどうかを指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>UDP のオフロードが有効になっているかどうかを指定します。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
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

 

 




