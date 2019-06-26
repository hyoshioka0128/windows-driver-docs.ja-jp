---
title: バグ チェック 0 xcd PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: PAGE_FAULT_BEYOND_END_OF_ALLOCATION のバグ チェックでは、0x000000CD の値を持ちます。 これは、システムがいくつかのドライバーのプールの割り当ての末尾を超えるメモリをアクセスすることを示します。
ms.assetid: ce506f92-94a9-4ef5-974b-32013410468a
keywords:
- バグ チェック 0 xcd PAGE_FAULT_BEYOND_END_OF_ALLOCATION
- PAGE_FAULT_BEYOND_END_OF_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_BEYOND_END_OF_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c6a2d015f1137445f1f31efec1f62e9d7390391
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367170"
---
# <a name="bug-check-0xcd-pagefaultbeyondendofallocation"></a>バグ チェック 0xCD:ページ\_フォールト\_を超えて\_エンド\_の\_割り当て


ページ\_フォールト\_を超えて\_エンド\_の\_割り当てのバグ チェックが 0x000000CD の値を持ちます。 これは、システムがいくつかのドライバーのプールの割り当ての末尾を超えるメモリをアクセスすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="pagefaultbeyondendofallocation-parameters"></a>ページ\_フォールト\_を超えて\_エンド\_の\_割り当てパラメーター


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
<td align="left"><p>参照されているメモリ アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>メモリ (わかる場合) を参照されているアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

割り当てられたドライバー *n*特別なプールからメモリのバイト数。 参照されているシステムでは、その後、複数の*n*このプールからのバイト数。 これは通常、システム ドライバーの同期の問題を示します。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

<a name="remarks"></a>注釈
-------

これで保護することはできません、 **- お試しくださいを除く**ハンドラー--プローブによってのみ保護できます。

 

 




