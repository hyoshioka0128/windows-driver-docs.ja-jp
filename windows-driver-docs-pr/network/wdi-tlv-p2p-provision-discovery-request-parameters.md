---
title: WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_PARAMETERS
description: WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_PARAMETERS では、Wi-fi プロビジョニング検出要求のパラメーターを含む TLV です。
ms.assetid: 938F9CA0-0B34-4507-86CC-731C969335F7
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_PROVISION_DISCOVERY_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e8f6d356dd6c7f9024e87c6516f3d645e33fd7db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362904"
---
# <a name="wditlvp2pprovisiondiscoveryrequestparameters"></a>WDI\_TLV\_P2P\_プロビジョニング\_検出\_要求\_パラメーター


WDI\_TLV\_P2P\_プロビジョニング\_検出\_要求\_パラメーターは、Wi-fi プロビジョニング検出要求のパラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x85

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型  | 説明                                                                                                                                                          |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | Wi-Fi Direct グループ機能のビットマスク。 ビットマスクは、Wi-Fi Direct technical specification 表 13 グループ機能のビットマップ定義で定義されているものと一致します。 |
| UINT8 | その上グループ機能のビットマップのビットは、オペレーティング システムによって設定されます。                                                                                  |

 

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

 

 




