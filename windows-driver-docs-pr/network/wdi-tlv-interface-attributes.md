---
title: WDI_TLV_INTERFACE_ATTRIBUTES
description: WDI_TLV_INTERFACE_ATTRIBUTES では、インターフェイスの属性を含む TLV です。
ms.assetid: A36AC0A7-6F5B-4461-841D-3B4C19BD49EB
ms.date: 07/18/2017
keywords:
- WDI_TLV_INTERFACE_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 553ea43355a1cec591f6a83d780b97369c93ca23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361743"
---
# <a name="wditlvinterfaceattributes"></a>WDI\_TLV\_インターフェイス\_属性


WDI\_TLV\_インターフェイス\_属性は、インターフェイスの属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x21

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                     |
|------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_インターフェイス\_機能**](wdi-tlv-interface-capabilities.md)  |                                |          | インターフェイスの機能です。                                                                                                                                                              |
| [**WDI\_TLV\_ファームウェア\_バージョン**](wdi-tlv-firmware-version.md)              |                                |          | ファームウェアのバージョンを示す ASCII 文字列。                                                                                                                                            |
| [**WDI\_TLV\_IHV\_非\_WDI\_OID\_一覧**](wdi-tlv-ihv-non-wdi-oids-list.md) |                                | x        | リストの非-WDI Oid、アダプターは、オペレーティング システムに提供する必要があります。 アダプターはオペレーティング システムで非-WDI Oid この一覧に一致するが既にフィルター処理すると想定する必要があります。 |

 

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

 

 




