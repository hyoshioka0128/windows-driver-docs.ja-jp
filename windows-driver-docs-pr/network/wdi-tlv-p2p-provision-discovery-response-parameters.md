---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_PARAMETERS では、プロビジョニング検出応答のパラメーターを含む TLV です。
ms.assetid: 0732C370-108E-4C9A-AF13-2B7D54AEB984
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_DISCOVERY_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 390728f8d9d58ac0e209a3cca45ec5621bfa3f9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362900"
---
# <a name="wditlvp2pprovisiondiscoveryresponseparameters"></a>WDI\_TLV\_P2P\_プロビジョニング\_検出\_応答\_パラメーター


WDI\_TLV\_P2P\_プロビジョニング\_検出\_応答\_パラメーターは、プロビジョニング検出応答のパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x113

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型  | 説明                                                                                                                                                           |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | Wi-Fi Direct グループ機能に対応するビットマスク。 ビットマスクは、Wi-fi P2P technical specification 表 13 グループ機能のビットマップ定義で定義されているものと一致します。 |
| UINT8 | 上記のグループ機能のビットマップのオペレーティング システムによって設定されるビットです。                                                                                            |

 

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

 

 




