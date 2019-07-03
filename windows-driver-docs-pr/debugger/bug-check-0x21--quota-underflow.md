---
title: バグ チェック 0x21 QUOTA_UNDERFLOW
description: QUOTA_UNDERFLOW のバグ チェックでは、0x00000021 の値を持ちます。 これは、クォータの料金を課金が以前よりも多くのクォータ、特定のブロックを返すことによって誤りがあることを示します。
ms.assetid: 41b1c93b-77e0-4baa-8eed-7a956e45d144
keywords:
- バグ チェック 0x21 QUOTA_UNDERFLOW
- QUOTA_UNDERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- QUOTA_UNDERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45b0427b81d0321e1fbb8a7c7ece763dd733ba39
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519594"
---
# <a name="bug-check-0x21-quotaunderflow"></a>バグ チェック 0x21:クォータ\_アンダー フロー


クォータ\_アンダー フローのバグ チェックが 0x00000021 の値を持ちます。 これは、クォータの料金を課金が以前よりも多くのクォータ、特定のブロックを返すことによって誤りがあることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="quotaunderflow-parameters"></a>クォータ\_アンダー フローのパラメーター


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
<td align="left"><p>このプロセスが最初に課金される、使用可能な場合。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>クォータの種類。 すべての可能なクォータの種類の値の一覧で、Ps.h Windows Driver Kit (WDK) でのヘッダー ファイルを参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>返されるクォータの初期量を課金されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>返されませんでしたクォータの残りの量。</p></td>
</tr>
</tbody>
</table>

 

 

 




