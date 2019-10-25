---
title: WDI_TLV_CONNECTION_SETTINGS
description: WDI_TLV_CONNECTION_SETTINGS は、OID_WDI_TASK_CONNECT の接続設定を含む TLV です。
ms.assetid: E08E895D-BFD6-496E-82FE-881FDDB0B88E
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECTION_SETTINGS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 88676a88acf0b2e36277d865253b0aa45bc596ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843386"
---
# <a name="wdi_tlv_connection_settings"></a>WDI\_TLV\_接続\_の設定


WDI\_TLV\_接続\_設定は、 [OID\_WDI\_TASK\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-connect)の接続設定を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x3F

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                         | 説明                                                                                                                                                                                                               |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                                        | これが初めての接続要求 (値 0) であるか、ローミング接続 (値 1) であるかを指定します。                                                                                                                   |
| UINT8                                                        | このが非ブロードキャスト Ssid を使用してネットワークに接続されているかどうかを指定します。 非表示のネットワークに接続する場合、この値は1です。                                                                                      |
| UINT8                                                        | これにより、dot11ExcludeUnencrypted MIB が設定されます。 この値が false (0) で、暗号アルゴリズムが WEP の場合、ポートは管理フレームのプライバシーフィールドを設定していない Ap に接続する必要があります。                             |
| UINT8                                                        | MFP が有効 (1) または無効 (0) かどうかを指定します。 ステーションは、この値が 1 (有効) に設定されている場合にのみ、アソシエーション要求で 802.11 w 機能をアドバタイズする必要があります。                                          |
| UINT8                                                        | ホスト FIPS モードが有効 (1) または無効 (0) であるかどうかを指定します。                                                                                                                                                               |
| [**WDI\_ASSOC\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32) | 移動に必要な理由を指定します。 この問題が発生した場合、 [NDIS\_STATUS\_WDI\_\_示さ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)れているため、ローミング\_必要があります。 |
| [**WDI\_ローミング\_トリガー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_roam_trigger) (UINT32) | このローミングが重要なローミングであるかどうかを指定します。これは、AP が BSS 遷移要求のアクションフレームで関連付け間近のビットを設定したためです。                                                                         |
| UINT8                                                        | 802.11 v BSS の移行がサポートされているかどうかを指定します。 このビットが1に設定されている場合、ステーションは、アソシエーション要求の拡張機能要素 (ビット 19) の BSS 遷移フィールドを1に設定する必要があります。                   |

 

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

 

 




