---
title: WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS では、Wi-Fi Direct 招待要求パラメーターを含む TLV です。
ms.assetid: CC9B0454-4522-4589-8E21-4986BAEBC6D0
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cac2e8c37aee93e87f664396de68dea854e321d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347232"
---
# <a name="wditlvp2pinvitationrequestparameters"></a>WDI\_TLV\_P2P\_招待\_要求\_パラメーター


WDI\_TLV\_P2P\_招待\_要求\_パラメーターは、Wi-Fi Direct 招待要求パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x7C

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT16</td>
<td>グループ所有者構成タイムアウト (ミリ秒単位) には。</td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>クライアント構成タイムアウト (ミリ秒単位)。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>招待は、Wi-Fi Direct の仕様で定義されたフラグです。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>招待要求の送信が招待をローカル グループの所有者であるかどうかを示すビット。
<p>有効な値とは、0 および 1 です。 このビットは、ローカルの GO に招待状の場合、1 に設定されます。</p></td>
</tr>
</tbody>
</table>

 

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

 

 




