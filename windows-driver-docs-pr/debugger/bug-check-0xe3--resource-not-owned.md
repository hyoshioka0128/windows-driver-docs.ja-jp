---
title: バグ チェック 0xE3 RESOURCE_NOT_OWNED
description: RESOURCE_NOT_OWNED のバグ チェックでは、0x000000E3 の値を持ちます。 これは、スレッドが所有せず、リソースを解放しようとしたことを示します。
ms.assetid: f0f47af6-cba0-42a0-912b-562f069d5b3e
keywords:
- バグ チェック 0xE3 RESOURCE_NOT_OWNED
- RESOURCE_NOT_OWNED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESOURCE_NOT_OWNED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fa5cd04d7c83ec572a7876a9c993fb5b2a85a9f
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518816"
---
# <a name="bug-check-0xe3-resourcenotowned"></a>バグ チェック 0xE3:リソース\_いない\_所有されています。


リソース\_いない\_所有されているバグ チェックが 0x000000E3 の値を持ちます。 これは、スレッドが所有せず、リソースを解放しようとしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="resourcenotowned-parameters"></a>リソース\_いない\_所有されているパラメーター


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
<td align="left"><p>リソースのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>スレッドのアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>所有者のテーブル (存在する場合) のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

 

 




