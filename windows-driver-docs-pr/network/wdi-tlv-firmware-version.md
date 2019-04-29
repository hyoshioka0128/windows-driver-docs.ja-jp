---
title: WDI_TLV_FIRMWARE_VERSION
description: WDI_TLV_FIRMWARE_VERSION では、ファームウェアのバージョンを含む TLV です。
ms.assetid: 31E61ACA-AF2F-4E5D-9448-363630A27E39
ms.date: 07/18/2017
keywords:
- WDI_TLV_FIRMWARE_VERSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a9d6bfbf23252c6c73afa8a9f93c4dfef7d068ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329630"
---
# <a name="wditlvfirmwareversion"></a>WDI\_TLV\_ファームウェア\_バージョン


WDI\_TLV\_ファームウェア\_バージョンは、ファームウェアのバージョンを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xF4

## <a name="length"></a>長さ


Char 型の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型     | 説明                                                     |
|----------|-----------------------------------------------------------------|
| char\[\] | ファームウェア バージョンは、null で終わる ASCII 文字列として格納します。 |

 

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

 

 




