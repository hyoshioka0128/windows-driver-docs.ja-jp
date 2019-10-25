---
title: WDI_TLV_SCAN_MODE
description: WDI_TLV_SCAN_MODE は、スキャンモードパラメーターを含む TLV です。
ms.assetid: 9F954B66-4F1D-48F2-9316-BE623DF0CAE6
ms.date: 07/18/2017
keywords:
- WDI_TLV_SCAN_MODE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f22f52d952e4a8761417810f744f618d2cd8c94e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841739"
---
# <a name="wdi_tlv_scan_mode"></a>WDI\_TLV\_SCAN\_モード


WDI\_TLV\_SCAN\_MODE は、スキャンモードパラメーターを含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x6

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                | 説明                                                                                                                                                                                                                       |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                               | フルスキャンの手順を繰り返す回数。 この値が0に設定されている場合は、タスクがホストによって中止されるまでスキャンを繰り返す必要があります。                                                                     |
| [**WDI\_SCAN\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_type)       | 実行するスキャンの種類を指定します。 WDI\_SCAN\_TYPE\_ACTIVE が設定されている場合、デバイスはアクティブなチャネルのみをスキャンする必要があります。                                                                                                |
| UINT8                                               | ライブ更新が必要かどうかを指定し、検出されたエントリが見つかった場合はそれを報告する必要があります。上記の推奨される調整ロジックを使用します。 Microsoft コンポーネントが BSS リストキャッシュを管理する場合、この値は常に true です。 |
| [**WDI\_SCAN\_トリガー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_trigger) | スキャンのトリガーを指定します。                                                                                                                                                                                               |

 

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

 

 




