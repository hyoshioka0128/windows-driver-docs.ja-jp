---
title: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES
description: WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES では、Wi-Fi Direct サービスのプロビジョニングの属性を含む TLV です。
ms.assetid: CA318E91-660A-4F17-827B-F27E18643CC6
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_SERVICE_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5570d2eb47afb79b9a2a90d081a1f2d90d641743
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539206"
---
# <a name="wditlvp2pprovisionserviceattributes"></a>WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性


WDI\_TLV\_P2P\_プロビジョニング\_サービス\_属性は、Wi-Fi Direct サービスのプロビジョニングの属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xC6

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 種類                                              | 説明                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | Wi-Fi Direct ステータス コード、Wi-Fi Direct の仕様で定義されています。                                                                            |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 以降の Wi-Fi Direct 接続のローカルの MAC アドレス。                                                                                              |
| UINT8                                             | 接続機能のビットマスク。                                                                                                                     |
| UINT32                                            | 機能の機能のビットマスク。                                                                                                                        |
| UINT32                                            | サービス インスタンスの提供情報 ID。                                                                                                         |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | サービス インスタンスのサービスのアドレス。                                                                                                          |
| UINT32                                            | サービスにセッションを一意に識別するセッション ID です。                                                                                    |
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | サービスにセッションを一意に識別するセッションのアドレス。                                                                               |
| UINT16                                            | 構成のタイムアウトをミリ秒単位で移動します。                                                                                                          |
| UINT16                                            | クライアント構成のタイムアウト (ミリ秒単位)。                                                                                                      |
| UINT8                                             | 永続的なグループを接続に使用するかどうかを示すフラグです。 フラグは、永続的なグループを使用する場合、1 に設定されます。                  |
| UINT8                                             | このフレームが後続のプロビジョニング検出の一部であることを示すフラグです。 フラグは、後続のプロビジョニングの検出の一部である場合、1 に設定されます。 |

 

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

 

 




