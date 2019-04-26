---
title: バグ チェック 0x127 PAGE_NOT_ZERO
description: PAGE_NOT_ZERO のバグ チェックでは、0x00000127 の値を持ちます。
ms.assetid: b6485307-191d-401a-8f2e-7f4a54a630f9
keywords:
- バグ チェック 0x127 PAGE_NOT_ZERO
- PAGE_NOT_ZERO
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PAGE_NOT_ZERO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f167d5930b3dd7558af9833f3a9264a002cf1183
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354802"
---
# <a name="bug-check-0x127-pagenotzero"></a>バグ チェック 0x127:ページ\_いない\_0


ページ\_いない\_0 個のバグ チェックが 0x00000127 の値を持ちます。 このバグ チェックでは、ゼロで埋められたはページがなかったことを示します。 このバグ チェックは、ハードウェア エラーのために発生する可能性がありますまたはオペレーティング システムの特権を持つコンポーネントがそれを解放した後、ページを変更します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="pagenotzero-parameters"></a>ページ\_いない\_0 個のパラメーター


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
<td align="left"><p>破損したページをマップする仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>物理的なページ数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0 (予約済み)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0 (予約済み)</p></td>
</tr>
</tbody>
</table>

 

 

 




