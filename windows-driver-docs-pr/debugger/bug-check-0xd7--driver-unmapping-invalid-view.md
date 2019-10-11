---
title: バグチェック 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
description: DRIVER_UNMAPPING_INVALID_VIEW のバグチェックの値は0x000000D7 です。 これは、ドライバーが、マップされていないアドレスのマッピングを解除しようとしていることを示します。
ms.assetid: 68075aa7-f579-49c7-a30a-a21312625ff9
keywords:
- バグチェック 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
- DRIVER_UNMAPPING_INVALID_VIEW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_UNMAPPING_INVALID_VIEW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 882a6175296b27d3f182065af8bb5db550876445
ms.sourcegitcommit: 0ba337ab671763e374c79b67f6730f1451c8615e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041336"
---
# <a name="bug-check-0xd7-driver_unmapping_invalid_view"></a>バグ チェック 0xD7:DRIVER @ NO__T-0UNMAPPING 解除 @ NO__T-1INVALID @ NO__T-2VIEW


ドライバー @ no__t-0UNMAPPING 解除 @ no__t-1INVALID @ no__t-2VIEW bug check の値は0x000000D7 です。 これは、ドライバーが、マップされていないアドレスのマッピングを解除しようとしていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_unmapping_invalid_view-parameters"></a>DRIVER @ no__t-0UNMAPPING 解除 @ no__t-1INVALID @ no__t-2VIEW Parameters


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
<td align="left"><p>マップ解除する仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>1:</strong>ビューがマップ解除されています</p>
<p><strong>2:</strong>ビューがコミットされています</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 [ [**Kb (スタックバックトレースの表示)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-) ] コマンドを使用してスタックトレースを取得します。エラーの原因となったドライバーは、スタックトレースから特定できます。

 

 




