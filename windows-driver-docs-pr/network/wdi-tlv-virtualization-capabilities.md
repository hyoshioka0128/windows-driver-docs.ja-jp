---
title: WDI_TLV_VIRTUALIZATION_CAPABILITIES
description: WDI_TLV_VIRTUALIZATION_CAPABILITIES では、仮想化機能を含む TLV です。
ms.assetid: D72E9984-7193-406C-8BA3-006E54400B30
ms.date: 07/18/2017
keywords:
- WDI_TLV_VIRTUALIZATION_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e5b3fae800f2d84916ff8a4ea3ce408cbc9fd745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376632"
---
# <a name="wditlvvirtualizationcapabilities"></a>WDI\_TLV\_VIRTUALIZATION\_機能


WDI\_TLV\_VIRTUALIZATION\_機能が仮想化機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x10

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型  | 説明                                                                                                                                                                                                                       |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | サポートされている ExtSTA ポートの数。                                                                                                                                                                                             |
| UINT8 | サポートされているポートを Wi-Fi Direct のグループ化の数。 この数は、ロール ポートのみを含める必要があります。 この値が 0 以外の場合、Wi-Fi Direct デバイスのポートがあると見なされます。                                               |
| UINT8 | サポートされているレガシ ExtAP ポートの数。                                                                                                                                                                                       |
| UINT8 | サポートされている同時 AP WFD/グループの所有者の最大数。                                                                                                                                                                 |
| UINT8 | デバイスで動作を保持できるデータ接続で同時に別のチャネルの最大数。 この制限は、スキャンと Wi-Fi Direct ネゴシエーションのような一時的なマルチ チャネルの操作を含めないでください。 |
| UINT8 | サポートされている同時 STA WFD/クライアントの最大数。                                                                                                                                                                     |

 

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

 

 




