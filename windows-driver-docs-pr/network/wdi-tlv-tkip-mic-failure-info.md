---
title: WDI_TLV_TKIP_MIC_FAILURE_INFO
description: WDI_TLV_TKIP_MIC_FAILURE_INFO は、TKIP MIC のエラー情報を含む TLV です。
ms.assetid: BBF168BE-6223-4C54-AFF5-17878D07EFBD
ms.date: 07/18/2017
keywords:
- WDI_TLV_TKIP_MIC_FAILURE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 76aa968fae4c3be1ce61d052e9bfe83db1a6c7b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357313"
---
# <a name="wditlvtkipmicfailureinfo"></a>WDI\_TLV\_TKIP\_MIC\_エラー\_情報


WDI\_TLV\_TKIP\_MIC\_エラー\_情報が [tkip] MIC のエラー情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x57

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                              | 説明                                                                                                                                                                                                                                              |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 暗号キーを指定の種類が [tkip] MIC のエラーが発生したことを検出します。 この値が 1 の場合は、[tkip] MIC のエラーが発生しました、既定の暗号キーを使用します。 この値が 0 の場合は、[tkip] MIC エラーが発生しました、キー マップ暗号キーを使用します。 |
| UINT32                                            | 既定のキーの配列では、暗号キーのインデックスを指定します。 有効な値の範囲は 0 ~ 3 です。                                                                                                                                                   |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) | MIC 検証に失敗したパケットを送信したピアの MAC アドレスを指定します。                                                                                                                                                          |

 

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

 

 




