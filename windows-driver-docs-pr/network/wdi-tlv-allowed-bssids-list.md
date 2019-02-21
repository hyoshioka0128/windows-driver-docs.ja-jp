---
title: WDI_TLV_ALLOWED_BSSIDS_LIST
description: WDI_TLV_ALLOWED_BSSIDS_LIST では、関連付けに使用することができる Bssid のリストを含む TLV です。
ms.assetid: A53C5EB2-1D77-4380-86C7-291D2BF4FCFC
ms.date: 07/18/2017
keywords:
- WDI_TLV_ALLOWED_BSSIDS_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: aa222b0cd05be2ae522a9467116816cb1481aff3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538662"
---
# <a name="wditlvallowedbssidslist"></a>WDI\_TLV\_許可\_BSSID\_一覧


WDI\_TLV\_許可\_BSSID\_リストは、関連付けに使用することができる Bssid のリストを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xC2

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 種類                                                  | 説明                                                   |
|-------------------------------------------------------|---------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | 関連付けに使用することができる Bssid の一覧。 |

 

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

 

 




