---
title: WDI_TLV_ACTION_FRAME_DEVICE_CONTEXT
description: WDI_TLV_ACTION_FRAME_DEVICE_CONTEXT では、アクションのフレームのデバイス コンテキストを含んでいる TLV です。
ms.assetid: D8AF374A-0AD0-4856-B05C-B8E3A3F1572B
ms.date: 07/18/2017
keywords:
- WDI_TLV_ACTION_FRAME_DEVICE_CONTEXT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 68fbfd57fee08bdcb3026e95bf2c3ab143d9354b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579637"
---
# <a name="wditlvactionframedevicecontext"></a>WDI\_TLV\_アクション\_フレーム\_デバイス\_コンテキスト


WDI\_TLV\_アクション\_フレーム\_デバイス\_コンテキストは、アクションのフレームのデバイス コンテキストを含んでいる TLV します。

## <a name="tlv-type"></a>TLV 型


0xAC

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                              |
|-----------|--------------------------------------------------------------------------|
| UINT8\[\] | アクションのフレームのデバイス コンテキストを含んでいる UINT8 要素の配列。 |

 

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

 

 




