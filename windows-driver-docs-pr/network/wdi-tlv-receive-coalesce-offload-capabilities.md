---
title: WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES
description: WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES は、Rx を含む TLV coalesce オフロード機能です。
ms.assetid: AF13B304-3E94-42EE-8BBB-107F5F238758
ms.date: 07/18/2017
keywords:
- WDI_TLV_RECEIVE_COALESCE_OFFLOAD_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7c58c4a917784767462bf5c60d7dc960463532fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359725"
---
# <a name="wditlvreceivecoalesceoffloadcapabilities"></a>WDI\_TLV\_受信\_COALESCE\_オフロード\_機能


WDI\_TLV\_受信\_COALESCE\_オフロード\_機能は、Rx を含む TLV がオフロード機能を結合します。

## <a name="tlv-type"></a>TLV 型


0xCE

## <a name="length"></a>長さ


サイズ (バイト単位) で、以下の値。

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
<td>UINT8</td>
<td>指定の IPv4 Rx に結合するかどうかが有効になっています。
<p>有効な値は 0 (無効) および 1 (有効です)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定の IPv6 の Rx に結合するかどうかが有効になっています。
<p>有効な値は 0 (無効) および 1 (有効です)。</p></td>
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

 

 




