---
title: WDI_TLV_SSID_OFFLOAD
description: WDI_TLV_SSID_OFFLOAD では、SSID と SSID についてのヒントを含む TLV です。
ms.assetid: 6CF08BEB-8CEE-4C07-B63B-7FAC7AEAB24F
ms.date: 07/18/2017
keywords:
- WDI_TLV_SSID_OFFLOAD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 88d0076d527ad57cba611b4f2e0e4e98331411a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366642"
---
# <a name="wditlvssidoffload"></a>WDI\_TLV\_SSID\_オフロード


WDI\_TLV\_SSID\_オフロードは、SSID と SSID についてのヒントを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x9E

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                 |
|------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid.md)                                       |                                |          | SSID です。                   |
| [**WDI\_TLV\_ユニキャスト\_アルゴリズム\_一覧**](wdi-tlv-unicast-algorithm-list.md) |                                |          | ユニキャスト アルゴリズムの一覧。 |
| [**WDI\_TLV\_チャネル\_一覧**](wdi-tlv-channel-list.md)                      |                                |          | チャネルの一覧。           |

 

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

 

 




