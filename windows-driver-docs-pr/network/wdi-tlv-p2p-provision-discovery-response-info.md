---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO
description: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO では、Wi-Fi Direct プロビジョニング検出応答情報を含む TLV です。
ms.assetid: EB7C4A5C-27D8-4A84-BC91-0DED51FB74C2
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b050269fe829f12a5db03f6576015983316ea334
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362810"
---
# <a name="wditlvp2pprovisiondiscoveryresponseinfo"></a>WDI\_TLV\_P2P\_プロビジョニング\_検出\_応答\_情報


WDI\_TLV\_P2P\_プロビジョニング\_検出\_応答\_情報は、Wi-Fi Direct プロビジョニング検出応答情報を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x87

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_プロビジョニング\_検出\_応答\_パラメーター**](wdi-tlv-p2p-provision-discovery-response-parameters.md) |                                |          | プロビジョニング検出応答のパラメーター。                                                                                                                                                                                            |
| [**WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性**](wdi-tlv-p2p-provision-service-attributes.md)                        |                                | x        | サービスのプロビジョニングの属性。                                                                                                                                                                                                       |
| [**WDI\_TLV\_P2P\_グループ\_ID**](wdi-tlv-p2p-group-id.md)                                                                 |                                | x        | Wi-Fi Direct サービスがサポートされている場合は、グループ ID。                                                                                                                                                                                      |
| [**WDI\_TLV\_P2P\_持続\_グループ\_ID**](wdi-tlv-p2p-persistent-group-id.md)                                          |                                | x        | 接続に使用する永続的なグループのグループの ip アドレス。 このフィールドは、永続的なグループにフラグを設定する場合に有効な[ **WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性**](wdi-tlv-p2p-provision-service-attributes.md)が 1 に設定します。 |
| [**WDI\_TLV\_P2P\_サービス\_セッション\_情報**](wdi-tlv-p2p-service-session-info.md)                                        |                                | x        | サービスのセッションの情報。                                                                                                                                                                                                        |

 

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

 

 




