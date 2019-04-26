---
title: バグ チェック 0x13B PASSIVE_INTERRUPT_ERROR
description: PASSIVE_INTERRUPT_ERROR のバグ チェックでは、0x0000013B の値を持ちます。 これは、カーネルのパッシブ レベル割り込みに関する問題が検出されたことを示します。
ms.assetid: 6C921FCB-B945-4909-BAD3-1DBD6E3CAA54
keywords:
- バグ チェック 0x13B PASSIVE_INTERRUPT_ERROR
- PASSIVE_INTERRUPT_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PASSIVE_INTERRUPT_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c48e1ee18d12101a77f9d04d49c792435e12f7ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353672"
---
# <a name="bug-check-0x13b-passiveinterrupterror"></a>バグ チェック 0x13B:パッシブ\_INTERRUPT\_エラー


パッシブ\_INTERRUPT\_エラーのバグ チェックが 0x0000013B の値を持ちます。 これは、カーネルのパッシブ レベル割り込みに関する問題が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="passiveinterrupterror-parameters"></a>パッシブ\_INTERRUPT\_エラー パラメーター


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
<td align="left"><p>検出されたエラーの種類</p>
0x1:ドライバーは、割り込みのスピン ロックを取得しようとしましたが、パッシブ レベル割り込みオブジェクトに渡されます。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パッシブ レベル割り込みに対する KINTERRUPT オブジェクトのアドレス。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">予約済み</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




