---
title: WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST
description: WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST では、セカンダリ デバイスの種類の一覧を含む TLV です。
ms.assetid: 278F3D2B-6729-4F7A-B3B2-B12D79C04530
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SECONDARY_DEVICE_TYPE_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c0c9d4317a159c6e413ef6b6097dafcf5232690b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573548"
---
# <a name="wditlvp2psecondarydevicetypelist"></a>WDI\_TLV\_P2P\_セカンダリ\_デバイス\_型\_一覧


WDI\_TLV\_P2P\_セカンダリ\_デバイス\_型\_リストは、セカンダリ デバイスの種類の一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x94

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_P2P\_デバイス\_型の要素。 0 の配列の長さが許可されます。

**注**  WDI\_P2P\_デバイス\_型は WDI 構造ではありません。 WDI TLV パーサー ジェネレーターで定義されているし、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 型                       | 説明                            |
|----------------------------|----------------------------------------|
| WDI\_P2P\_デバイス\_型\[\] | Wi-Fi Direct デバイスの種類の配列。 |

 

WDI\_P2P\_デバイス\_型は、次の要素で構成されます。

| 型       | 説明                                   |
|------------|-----------------------------------------------|
| UINT16     | 主要な型のカテゴリの id。                    |
| UINT8\[4\] | この種類のデバイスに割り当てられている OUI します。 |
| UINT16     | サブカテゴリの id。                           |

 

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

 

 




