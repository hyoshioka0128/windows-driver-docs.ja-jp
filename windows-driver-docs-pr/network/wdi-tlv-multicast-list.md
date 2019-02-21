---
title: WDI_TLV_MULTICAST_LIST
description: WDI_TLV_MULTICAST_LIST では、マルチキャスト MAC アドレスの配列を含む TLV です。
ms.assetid: 5023557A-1BC5-4A4E-A77C-20353C0CA3FD
ms.date: 07/18/2017
keywords:
- WDI_TLV_MULTICAST_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ce3dae46090326fc1479ccd050fd06532c8c15b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559432"
---
# <a name="wditlvmulticastlist"></a>WDI\_TLV\_マルチキャスト\_一覧


WDI\_TLV\_マルチキャスト\_リストは、マルチキャスト MAC アドレスの配列を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x6A

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 種類                                                  | 説明                          |
|-------------------------------------------------------|--------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | マルチキャスト MAC の配列について説明します。 |

 

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

 

 




