---
title: バグ チェック 0 xbf MUTEX_ALREADY_OWNED
description: MUTEX_ALREADY_OWNED のバグ チェックでは、0x000000BF の値を持ちます。 これは、ミュー テックスの所有権を取得しようとしています。 スレッドが既に所有されていることを示します。
ms.assetid: 0008c6eb-3add-4169-b29a-6fe4d77c5c9e
keywords:
- バグ チェック 0 xbf MUTEX_ALREADY_OWNED
- MUTEX_ALREADY_OWNED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUTEX_ALREADY_OWNED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d9a5e33a175cc4745dcaa96cb1411ce2ddba8e1e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518975"
---
# <a name="bug-check-0xbf-mutexalreadyowned"></a>バグ チェック 0xBF:ミュー テックス\_ALREADY\_所有されています。


ミュー テックス\_ALREADY\_所有されているバグ チェックが 0x000000BF の値を持ちます。 これは、ミュー テックスの所有権を取得しようとしています。 スレッドが既に所有されていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="mutexalreadyowned-parameters"></a>ミュー テックス\_ALREADY\_所有されているパラメーター


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
<td align="left"><p>ミュー テックスのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラーが発生したスレッド</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

 

 




