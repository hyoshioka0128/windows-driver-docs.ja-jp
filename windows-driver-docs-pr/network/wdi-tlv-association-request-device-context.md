---
title: WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT
description: WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT では、入力方向の関連付け要求に応答を送信するホストが決定した場合、ポートに下位へ渡されるベンダー固有の情報を含む TLV です。
ms.assetid: 5C684769-77A0-446D-81F6-A90E54806A1F
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_REQUEST_DEVICE_CONTEXT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7938af034d1300c284ad7ae0f3320866a9aec07e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539609"
---
# <a name="wditlvassociationrequestdevicecontext"></a>WDI\_TLV\_アソシエーション\_要求\_デバイス\_コンテキスト


WDI\_TLV\_アソシエーション\_要求\_デバイス\_コンテキストは、受信メッセージに応答を送信するホストが決定した場合、ポートに下位へ渡されるベンダー固有の情報を含む TLVアソシエーションの要求。

## <a name="tlv-type"></a>TLV 型


0x72

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 種類      | 説明                                                                                                                           |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 入力方向の関連付け要求に応答を送信するホストが決定した場合、ポートに下位へ渡されるベンダー固有の情報。 |

 

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

 

 




