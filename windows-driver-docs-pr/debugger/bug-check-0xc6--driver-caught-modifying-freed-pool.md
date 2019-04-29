---
title: バグ チェック 0xC6 DRIVER_CAUGHT_MODIFYING_FREED_POOL
description: DRIVER_CAUGHT_MODIFYING_FREED_POOL のバグ チェックでは、0x000000C6 の値を持ちます。 これは、ドライバーが解放されたメモリ プールへのアクセスを試行したことを示します。
ms.assetid: a5df3612-549d-4cf1-b3e1-4e5efad8ce88
keywords:
- バグ チェック 0xC6 DRIVER_CAUGHT_MODIFYING_FREED_POOL
- DRIVER_CAUGHT_MODIFYING_FREED_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CAUGHT_MODIFYING_FREED_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba18a6c3d20937abf6c64160285b63b9323283a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324672"
---
# <a name="bug-check-0xc6-drivercaughtmodifyingfreedpool"></a>バグ チェック 0xC6:ドライバー\_例外が発生しました\_変更\_FREED\_プール


ドライバー\_例外が発生しました\_変更\_FREED\_プールのバグ チェックが 0x000000C6 の値を持ちます。 これは、ドライバーが解放されたメモリ プールへのアクセスを試行したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="drivercaughtmodifyingfreedpool-parameters"></a>ドライバー\_例外が発生しました\_変更\_FREED\_プールのパラメーター


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
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>カーネル モード</p>
<p><strong>1:</strong>ユーザー モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

障害のあるコンポーネントが現在のカーネル スタックに表示されます。 このドライバーが、置き換えるか、またはデバッグする必要があります。

 

 




