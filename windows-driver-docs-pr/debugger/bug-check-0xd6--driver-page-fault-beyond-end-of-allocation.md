---
title: Bug Check 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION のバグ チェックでは、0x000000D6 の値を持ちます。 これは、そのプールの割り当ての末尾を越えるアクセス ドライバーのメモリを示します。
ms.assetid: 939165dc-3052-4de7-88fd-25d4a7e82945
keywords:
- Bug Check 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
- DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 38deede965ff4eca12381d2b3f36f8c5a9c61ad4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371732"
---
# <a name="bug-check-0xd6-driverpagefaultbeyondendofallocation"></a>バグ チェック 0xD6:ドライバー\_ページ\_フォールト\_を超えて\_エンド\_の\_割り当て


ドライバー\_ページ\_フォールト\_を超えて\_エンド\_の\_割り当てのバグ チェックが 0x000000D6 の値を持ちます。 これは、そのプールの割り当ての末尾を越えるアクセス ドライバーのメモリを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="driverpagefaultbeyondendofallocation-parameters"></a>ドライバー\_ページ\_フォールト\_を超えて\_エンド\_の\_割り当てパラメーター


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

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) *KiBugCheckDriver*します。

<a name="cause"></a>原因
-----

割り当てられたドライバー *n*バイトのメモリから参照されていると複数の*n*バイト。 Driver Verifier**特別なプール**オプションは、この違反を検出しました。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

<a name="remarks"></a>注釈
-------

これで保護することはできません、 **- お試しくださいを除く**ハンドラー--プローブによってのみ保護できます。

 

 




