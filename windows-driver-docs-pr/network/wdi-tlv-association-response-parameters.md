---
title: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS は、OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE のアソシエーションの応答パラメーターを含む TLV です。
ms.assetid: FB116762-2064-48FA-B630-D5AE54657D10
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 170bb13c630e950299dc08604f6221f4870490d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343181"
---
# <a name="wditlvassociationresponseparameters"></a>WDI\_TLV\_アソシエーション\_応答\_パラメーター


WDI\_TLV\_アソシエーション\_応答\_パラメーターがのアソシエーションの応答パラメーターを含む TLV [OID\_WDI\_タスク\_送信\_アジア太平洋\_アソシエーション\_応答](https://msdn.microsoft.com/library/windows/hardware/dn925960)します。

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

 

 




