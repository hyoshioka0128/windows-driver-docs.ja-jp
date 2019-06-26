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
ms.openlocfilehash: ad8c124b4f0b83e1e2c79ce9a0a3c5b0595b937d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362240"
---
# <a name="bug-check-0x13b-passiveinterrupterror"></a>バグ チェック 0x13B:パッシブ\_INTERRUPT\_エラー


パッシブ\_INTERRUPT\_エラーのバグ チェックが 0x0000013B の値を持ちます。 これは、カーネルのパッシブ レベル割り込みに関する問題が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


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

 

 

 




