---
title: バグ チェック 0xD8 DRIVER_USED_EXCESSIVE_PTES
description: DRIVER_USED_EXCESSIVE_PTES のバグ チェックでは、0x000000D8 の値を持ちます。 これがない複数のシステム ページ テーブル エントリ (PTE) の残りを示します。
ms.assetid: a11212eb-8dd7-49f3-9b23-237ed88b9cff
keywords:
- バグ チェック 0xD8 DRIVER_USED_EXCESSIVE_PTES
- DRIVER_USED_EXCESSIVE_PTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_USED_EXCESSIVE_PTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22f8c548bd0cea54c03e4c99a4f5f9bfa273e9df
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518855"
---
# <a name="bug-check-0xd8-driverusedexcessiveptes"></a>バグ チェック 0xD8:ドライバー\_使用\_の過剰な\_PTE


ドライバー\_使用\_の過剰な\_PTE バグ チェックが 0x000000D8 の値を持ちます。 これがない複数のシステム ページ テーブル エントリ (PTE) の残りを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="driverusedexcessiveptes-parameters"></a>ドライバー\_使用\_の過剰な\_PTE パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>(Unicode 文字列)、エラーの原因となったドライバーの名前へのポインターまたは 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>(パラメーター 1 が 0 以外の場合)、エラーの原因となったドライバーによって使用される Pte の数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>合計空きシステム Pte</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>システム Pte を合計します。</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

これは通常、正しくクリーンアップそのメモリを使用していないドライバーが原因です。 パラメーター 1 では、ほとんどの Pte が使用するドライバーを示します。 ドライバーのバグ チェック原因となった実際には、呼び出し履歴が表示されます。

<a name="resolution"></a>解決方法
----------

両方のドライバーは、修正する必要があります。 システム Pte の合計数が大きく必要もあります。

 

 




