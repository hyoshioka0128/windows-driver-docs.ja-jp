---
title: WDI_TLV_LINK_QUALITY_BAR_MAP
description: WDI_TLV_LINK_QUALITY_BAR_MAP では、信号の品質、Wi-fi 信号の強さバーへのマッピングを格納する TLV です。
ms.assetid: 35E073F4-D372-466A-98FF-0AAB1695284E
ms.date: 07/18/2017
keywords:
- WDI_TLV_LINK_QUALITY_BAR_MAP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ae8f9386f063b706ebd69bab342a3208b5c618a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572975"
---
# <a name="wditlvlinkqualitybarmap"></a>WDI\_TLV\_リンク\_品質\_バー\_マップ


WDI\_TLV\_リンク\_品質\_バー\_マップは、信号の品質、Wi-fi 信号の強さバーへのマッピングを格納する TLV します。

## <a name="tlv-type"></a>TLV 型


0xD8

## <a name="length"></a>長さ


WDI の配列のサイズをバイト単位で\_リンク\_品質\_バー\_マップ\_パラメーター要素。 配列には、1 つ以上の要素を含める必要があります。

**注**  WDI\_リンク\_品質\_バー\_マップ\_パラメーターは、WDI 構造ではありません。 WDI TLV パーサー ジェネレーターで定義されているし、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 型                                         | 説明                                         |
|----------------------------------------------|-----------------------------------------------------|
| WDI\_リンク\_品質\_バー\_マップ\_パラメーター\[\] | マッピング パラメーター バー信号の強さの配列。 |

 

WDI\_リンク\_品質\_バー\_マップ\_パラメーターは、次の要素で構成されます。

| 型  | 説明                                                                  |
|-------|------------------------------------------------------------------------------|
| UINT8 | 制限リンク品質の低下 (0-100) の現在の信号強度バー。    |
| UINT8 | 現在の信号強度バーのリンクの品質 (0-100) の上限値。 |
| UINT8 | 信号強度のバーの数。                                              |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




