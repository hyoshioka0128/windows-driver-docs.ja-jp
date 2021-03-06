---
title: WDI_TLV_CONNECTION_SETTINGS
description: WDI_TLV_CONNECTION_SETTINGS は、OID_WDI_TASK_CONNECT の接続設定を含む TLV です。
ms.assetid: E08E895D-BFD6-496E-82FE-881FDDB0B88E
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECTION_SETTINGS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 287246ab51fc791915dba41cd492f03ff262702a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384526"
---
# <a name="wditlvconnectionsettings"></a>WDI\_TLV\_接続\_設定


WDI\_TLV\_接続\_設定は、の接続設定を含む TLV [OID\_WDI\_タスク\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-connect)します。

## <a name="tlv-type"></a>TLV 型


0x3F

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                         | 説明                                                                                                                                                                                                               |
|--------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                                        | これは、初回の接続要求 (0 の値) またはローミング接続 (1 の値) を指定します。                                                                                                                   |
| UINT8                                                        | 非表示/非ブロードキャストの Ssid を持つネットワークへの接続を指定します。 非表示のネットワークに接続するときに、この値は 1 です。                                                                                      |
| UINT8                                                        | これには、dot11ExcludeUnencrypted MIB を設定します。 この値が false (0) と、暗号アルゴリズムは、WEP、ポートは、管理フレームで、[プライバシー] フィールドを設定しないでください Ap に接続する必要があります。                             |
| UINT8                                                        | MFP が有効になっている (1) か無効 (0) を指定します。 ステーションは、その 802.11w をアドバタイズする必要があります、アソシエーションに機能がこの設定は 1 (有効) 場合にのみを要求します。                                          |
| UINT8                                                        | ホスト FIPS モードが有効になっている (1) か無効 (0) を指定します。                                                                                                                                                               |
| [**WDI\_ASSOC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status) (UINT32) | ローミングの必要な理由を指定します。 ためにこれがトリガーされる場合[NDIS\_状態\_WDI\_を示す値\_ローミング\_必要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)、ローミング indication から理由が含まれます。 |
| [**WDI\_ローミング\_トリガー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_roam_trigger) (UINT32) | AP BSS 切り替え要求アクション フレームの関連付けの解除が迫っていないかのビットを設定されているために、このローミングが重要なローミングがかどうかを指定します。                                                                         |
| UINT8                                                        | 指定する場合 802.11v BSS 移行がサポートされています。 このビットが 1 に設定されている場合、ステーションは、関連の要求で 1 に拡張機能要素 (ビット 19) の BSS 遷移フィールドを設定する必要があります。                   |

 

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

 

 




