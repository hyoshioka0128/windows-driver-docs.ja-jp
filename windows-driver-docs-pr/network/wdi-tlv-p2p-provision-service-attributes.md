---
title: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES
description: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES は、Wi-fi Direct プロビジョンサービス属性を含む TLV です。
ms.assetid: CA318E91-660A-4F17-827B-F27E18643CC6
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 90098dd89339c0c3820efb4258c8af563410c3b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845127"
---
# <a name="wdi_tlv_p2p_provision_service_attributes"></a>WDI\_TLV\_P2P\_\_サービス\_属性のプロビジョニング


WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性は、Wi-fi Direct プロビジョニングサービス属性を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xC6

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                              | 説明                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-fi direct 仕様で定義されている wi-fi ダイレクトステータスコード。                                                                            |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 今後の Wi-fi 直接接続用のローカル MAC アドレス。                                                                                              |
| UINT8                                             | 接続機能のビットマスク。                                                                                                                     |
| UINT32                                            | 機能のビットマスク。                                                                                                                        |
| UINT32                                            | サービスインスタンスの提供情報 ID。                                                                                                         |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | サービスインスタンスのサービスアドレス。                                                                                                          |
| UINT32                                            | サービスに対するセッションを一意に識別するセッション ID。                                                                                    |
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | サービスに対するセッションを一意に識別するセッションアドレス。                                                                               |
| UINT16                                            | 構成のタイムアウトをミリ秒単位で設定します。                                                                                                          |
| UINT16                                            | クライアント構成のタイムアウト (ミリ秒)。                                                                                                      |
| UINT8                                             | 固定グループが接続に使用されるかどうかを示すフラグです。 永続化グループが使用される場合、フラグは1に設定されます。                  |
| UINT8                                             | このフレームが後続のプロビジョニング検出に含まれるかどうかを示すフラグ。 フラグは、後続のプロビジョニング検出の一部である場合は1に設定されます。 |

 

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

 

 




