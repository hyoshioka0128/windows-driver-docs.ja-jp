---
title: WDI_TLV_BSSID_INFO
description: WDI_TLV_BSSID_INFO は、BSSID 情報を含む TLV です。
ms.assetid: C9E2B2D5-16CA-438D-AD86-1FA4F4F11CD1
ms.date: 07/18/2017
keywords:
- WDI_TLV_BSSID_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 80bc47d204ad03a02f4773b4b142aac491b797f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535365"
---
# <a name="wditlvbssidinfo"></a>WDI\_TLV\_BSSID\_情報


WDI\_TLV\_BSSID\_情報が BSSID 情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x120

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類  | 説明                                                                                                                                                                                                                                                                                                                               |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | アジア太平洋経由で到達可能です。 有効な値は 1 (できない)、2 (不明) と 3 (到達) します。                                                                                                                                                                                                                                                      |
| UINT8 | セキュリティ。 これは、1 に設定されている場合は、現在の関連付けの STA で使用されるこの BSSID で識別される AP が同じセキュリティのプロビジョニングをサポートすることを示します。 0 に設定すると、いずれか、この AP が同一のセキュリティのプロビジョニングをサポートしていないか、この時点で、セキュリティ情報がご利用いただけませんことを示します。 |
| UINT8 | ビットのキーのスコープ。 1 に設定されている場合は、アジア太平洋のこの BSSID によって示されますが、レポートを送信 AP として同じ認証子を示します。 このビットが 0 に設定されている場合は、個別ユーザー認証システムを示します。 または情報をご利用いただけません。                                                                                                |
| UINT8 | これは、dot11SpectrumManagementRequired が true の場合、1 に設定されます。                                                                                                                                                                                                                                                                              |
| UINT8 | これは、dot11QosOptionImplemented が true の場合、1 に設定されます。                                                                                                                                                                                                                                                                                    |
| UINT8 | AP では、dot11APSDOptionImplemented が true の場合と、それ以外の場合 0 に設定するときに、機能情報フィールド内の 1 に APSD サブフィールドを設定します。                                                                                                                                                                                            |
| UINT8 | これは、dot11RadioMeasurementActivated が true の場合、1 に設定されます。                                                                                                                                                                                                                                                                               |
| UINT8 | これは、dot11DelayedBlockAckOptionImplemented が true の場合、1 に設定されます。                                                                                                                                                                                                                                                                        |
| UINT8 | これは、dot11ImmediateBlockAckOptionImplemented が true の場合、1 に設定されます。                                                                                                                                                                                                                                                                      |
| UINT8 | これは、この BSSID によって表される AP mde ファイルをビーコン フレームに含まれている場合、1 に設定されます。                                                                                                                                                                                                                                                |
| UINT8 | これは、この BSSID によって表される AP がそのビーコンで HT 機能要素を含む、HT AP であることを示す 1 に設定されます。                                                                                                                                                                                                      |

 

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

 

 




