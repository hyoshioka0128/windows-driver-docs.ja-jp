---
title: WDI_TLV_P2P_DEVICE_INFO_PARAMETERS
description: WDI_TLV_P2P_DEVICE_INFO_PARAMETERS では、Wi-Fi Direct デバイス情報パラメーターを含む TLV です。
ms.assetid: A0B1AC85-5F99-4674-A1C4-E25554BDD89F
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_INFO_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c34165d616b00bed68c2d78ad056b02cc696c0c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366346"
---
# <a name="wditlvp2pdeviceinfoparameters"></a>WDI\_TLV\_P2P\_デバイス\_情報\_パラメーター


WDI\_TLV\_P2P\_デバイス\_情報\_パラメーターは、Wi-Fi Direct デバイス情報パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x86

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型       | 説明                                            |
|------------|--------------------------------------------------------|
| UINT8\[6\] | ピアの Wi-Fi Direct デバイス アドレス。           |
| UINT16     | デバイスでサポートされる構成メソッド。     |
| UINT16     | プライマリ デバイスの種類:主要な型のカテゴリの識別子です。    |
| UINT8\[4\] | プライマリ デバイスの種類:この種類のデバイスに割り当てられている OUI します。 |
| UINT16     | プライマリ デバイスの種類:Subcategory 型識別子。      |

 

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

 

 




