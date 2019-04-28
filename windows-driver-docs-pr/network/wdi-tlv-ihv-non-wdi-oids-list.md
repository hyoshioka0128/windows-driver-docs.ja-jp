---
title: WDI_TLV_IHV_NON_WDI_OIDS_LIST
description: WDI_TLV_IHV_NON_WDI_OIDS_LIST では、リストの非-WDI Oid、アダプターは、オペレーティング システムに提供する必要があるを含む TLV です。
ms.assetid: 84929276-F098-4C24-A499-E252D5FB71A6
ms.date: 07/18/2017
keywords:
- WDI_TLV_IHV_NON_WDI_OIDS_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3d031a2495a8cedf6195ac4ea9438862a3c8b029
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365387"
---
# <a name="wditlvihvnonwdioidslist"></a>WDI\_TLV\_IHV\_非\_WDI\_OID\_一覧


WDI\_TLV\_IHV\_非\_WDI\_OID\_リストの非-WDI Oid、アダプターは、オペレーティング システムに提供する必要があるリストを含む TLV は、します。

## <a name="tlv-type"></a>TLV 型


0x104

## <a name="length"></a>長さ


Uint32 型の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型       | 説明                                                                                                                                                                                       |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32\[\] | リストの非-WDI Oid、アダプターは、オペレーティング システムに提供する必要があります。 アダプターはオペレーティング システムで非-WDI Oid この一覧に一致するが既にフィルター処理すると想定する必要があります。 |

 

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

 

 




