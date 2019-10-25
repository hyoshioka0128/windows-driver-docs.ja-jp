---
title: WDI_TLV_TKIP_MIC_FAILURE_INFO
description: WDI_TLV_TKIP_MIC_FAILURE_INFO は、TKIP-MIC エラー情報を含む TLV です。
ms.assetid: BBF168BE-6223-4C54-AFF5-17878D07EFBD
ms.date: 07/18/2017
keywords:
- WDI_TLV_TKIP_MIC_FAILURE_INFO ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 0c1734d4dcc6f702bc19107a6a0bdaef1a05a981
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841722"
---
# <a name="wdi_tlv_tkip_mic_failure_info"></a>WDI\_TLV\_TKIP\_MIC\_エラー\_情報


WDI\_TLV\_TKIP\_MIC\_FAILURE\_INFO は、TKIP-MIC エラー情報を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x57

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                                                                                                                              |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | TKIP エラーが発生したことを検出した暗号キーの種類を指定します。 この値が1の場合、既定の暗号キーを使用して TKIP エラーが検出されました。 この値が0の場合、キーマッピング暗号キーを使用して TKIP エラーが検出されました。 |
| UINT32                                            | 既定のキー配列内の暗号キーのインデックスを指定します。 有効な値の範囲は 0 ~ 3 です。                                                                                                                                                   |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | MIC 検証に失敗したパケットを送信したピアの MAC アドレスを指定します。                                                                                                                                                          |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




