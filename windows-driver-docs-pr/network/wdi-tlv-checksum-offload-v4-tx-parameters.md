---
title: WDI_TLV_CHECKSUM_OFFLOAD_V4_TX_PARAMETERS (0XD1)
description: WDI_TLV_CHECKSUM_OFFLOAD_V4_TX_PARAMETERS では、IPv4 の Tx チェックサム オフロード用のパラメーターを含む TLV です。
ms.assetid: EA862CDA-5FF4-4C5F-A522-224714640F34
ms.date: 07/18/2017
keywords:
- WDI_TLV_CHECKSUM_OFFLOAD_V4_TX_PARAMETERS (0xD1) ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 244fd16ea80ae70292ce9546201d313882eb245a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353179"
---
# <a name="wditlvchecksumoffloadv4txparameters-0xd1"></a>WDI\_TLV\_チェックサム\_オフロード\_V4\_TX\_パラメーター (0xD1)


WDI\_TLV\_チェックサム\_オフロード\_V4\_TX\_パラメーターは、IPv4 の Tx チェックサム オフロード用のパラメーターを含む TLV します。

記載されている機能の値が報告[ **NDIS\_TCP\_IP\_チェックサム\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff567878)します。 NDIS を使用して、\_オフロード\_いない\_サポートと NDIS\_オフロード\_を介して機能を指定する際にサポートされている[OID\_WDI\_GET\_アダプター\_機能](https://msdn.microsoft.com/library/windows/hardware/dn925838)します。

## <a name="tlv-type"></a>TLV 型


0xD1

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
<td>カプセル化の設定です。 有効な値は次のとおりです。
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>IP のオプションを checksum のオフロードがサポートされているかどうかを指定します。</td>
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
<tr class="even">
<td>UINT32</td>
<td>IP チェックサムが有効になっているかどうかを指定します。</td>
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

 

 




