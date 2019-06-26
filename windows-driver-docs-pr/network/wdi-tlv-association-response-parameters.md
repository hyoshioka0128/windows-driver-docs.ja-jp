---
title: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS は、OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE のアソシエーションの応答パラメーターを含む TLV です。
ms.assetid: FB116762-2064-48FA-B630-D5AE54657D10
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1266b946d737622a64340caf75ecfd3e0ae6702b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354935"
---
# <a name="wditlvassociationresponseparameters"></a>WDI\_TLV\_アソシエーション\_応答\_パラメーター


WDI\_TLV\_アソシエーション\_応答\_パラメーターがのアソシエーションの応答パラメーターを含む TLV [OID\_WDI\_タスク\_送信\_アジア太平洋\_アソシエーション\_応答](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-send-ap-association-response)します。

## <a name="tlv-type"></a>TLV 型


0x97

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
<td>UINT8</td>
<td>アソシエーションの要求を受け入れるかどうかを指定します。
<p>有効な値は 0 (受け入れない) と 1 (そのまま使用)。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>理由コードを指定します。 場合の要求の設定を受け入れるを 0 には、このフィールドは、ピア アダプターに返送する理由コードを提供します。</td>
</tr>
</tbody>
</table>

 

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

 

 




