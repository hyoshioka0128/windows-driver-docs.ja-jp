---
title: バグ チェック 0xE7 INVALID_FLOATING_POINT_STATE
description: INVALID_FLOATING_POINT_STATE のバグ チェックでは、0x000000E7 の値を持ちます。 これは、スレッドの保存された浮動小数点状態が無効であることを示します。
ms.assetid: 71a61132-cb7f-4618-b3d5-95602e52c098
keywords:
- バグ チェック 0xE7 INVALID_FLOATING_POINT_STATE
- INVALID_FLOATING_POINT_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_FLOATING_POINT_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bfd6786c9d4b66663d91758ebfa7bd8a46e60399
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902678"
---
# <a name="bug-check-0xe7-invalidfloatingpointstate"></a>バグ チェック 0xE7:無効な\_浮動\_ポイント\_状態


無効な\_浮動\_ポイント\_状態のバグ チェックが 0x000000E7 の値を持ちます。 これは、スレッドの保存された浮動小数点状態が無効であることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="invalidfloatingpointstate-parameters"></a>無効な\_浮動\_ポイント\_状態パラメーター


パラメーター 1 がどの有効性を示すチェックに失敗しました。 パラメーター 4 には使用されません。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>フラグ フィールド</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>保存されたコンテキストの flags フィールドが無効です。 FLOAT_SAVE_VALID が設定されていないか、いくつかの予約済みビットが 0 以外の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>保存した IRQL</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>現在のプロセッサの IRQL でない浮動小数点のコンテキストの保存時と同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>この浮動小数点のコンテキストを所有するスレッドの保存済みのアドレス</p></td>
<td align="left"><p>現在のスレッド</p></td>
<td align="left"><p>保存されたコンテキストは、現在のスレッドに属していません。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

以前に保存したスレッドの浮動小数点状態を復元するときに、無効になる状態が見つかりました。

パラメーター 1 がどの有効性を示すチェックに失敗しました。

 

 




