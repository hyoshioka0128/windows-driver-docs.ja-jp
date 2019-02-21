---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_INFO
description: WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_INFO では、Wi-Fi Direct のプロビジョニングの検出要求の情報を含む TLV です。
ms.assetid: C71F2FA9-2255-45E9-83CD-FA8DBEF5EA74
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cac289c152243e71c6ab03c98518bdfd88eb763a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528506"
---
# <a name="wditlvp2pprovisiondiscoveryrequestinfo"></a>WDI\_TLV\_P2P\_プロビジョニング\_検出\_要求\_情報


WDI\_TLV\_P2P\_プロビジョニング\_検出\_要求\_情報は、Wi-Fi Direct のプロビジョニングの検出要求の情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x83

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                                   | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_プロビジョニング\_検出\_要求\_パラメーター**](wdi-tlv-p2p-provision-discovery-request-parameters.md) |                                |          | Wi-Fi Direct のプロビジョニングの検出要求のパラメーター。                                                                                                                                                                                |
| [**WDI\_TLV\_P2P\_グループ\_ID**](wdi-tlv-p2p-group-id.md)                                                               |                                | X        | Wi-Fi Direct 移動対象のグループ ID。 グループ ID は省略可能です。 Wi-Fi Direct サービスの場合、ローカル Wi-Fi Direct GO 用のリモート側が参加するグループ ID です。                                       |
| [**WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性**](wdi-tlv-p2p-provision-service-attributes.md)                      |                                | X        | Wi-Fi Direct サービスのプロビジョニングの属性。                                                                                                                                                                                          |
| [**WDI\_TLV\_P2P\_持続\_グループ\_ID**](wdi-tlv-p2p-persistent-group-id.md)                                        |                                | X        | 接続に使用する永続的なグループのグループの ip アドレス。 このフィールドは、永続的なグループにフラグを設定する場合に有効な[ **WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性**](wdi-tlv-p2p-provision-service-attributes.md)が 1 に設定します。 |
| [**WDI\_TLV\_P2P\_サービス\_セッション\_情報**](wdi-tlv-p2p-service-session-info.md)                                      |                                | X        | サービスのセッションの情報。 このフィールドは有効な場合は[ **WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性**](wdi-tlv-p2p-provision-service-attributes.md)が存在します。                                                                       |

 

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

 

 




