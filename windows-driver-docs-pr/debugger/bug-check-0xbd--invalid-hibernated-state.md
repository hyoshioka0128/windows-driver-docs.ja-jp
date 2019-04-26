---
title: バグ チェック 0xBD INVALID_HIBERNATED_STATE
description: INVALID_HIBERNATED_STATE のバグ チェックでは、0x000000BD の値を持ちます。
ms.assetid: DB386A20-EE6F-4E2B-8FFD-51CCE0A8AEAC
keywords:
- バグ チェック 0xBD INVALID_HIBERNATED_STATE
- INVALID_HIBERNATED_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_HIBERNATED_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d480226a052f2d689f1fdf032d1f554a0090106
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347117"
---
# <a name="bug-check-0xbd-invalidhibernatedstate"></a>バグ チェック 0xBD:無効な\_HIBERNATED\_状態


無効な\_HIBERNATED\_状態のバグ チェックが 0x000000BD の値を持ちます。 これは、休止状態のメモリのイメージが現在のハードウェア構成と一致しないことを示します。 このバグチェックが行われるは、システムが休止状態から再開し、は、システムの休止中に、ハードウェアが変更されたことを検出します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="invalidhibernatedstate-parameters"></a>無効な\_HIBERNATED\_状態パラメーター


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
<td align="left">1</td>
<td align="left"><p>ハードウェアが無効です。</p>
<p>1 :インストールされているプロセッサの数が以前よりも少ないが、休止状態</p>
<p>Param 2 の値。休止状態の前にプロセッサの数</p>
<p>パラメーター 3 の値。休止状態の後のプロセッサの数</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 ごと</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 ごと</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




