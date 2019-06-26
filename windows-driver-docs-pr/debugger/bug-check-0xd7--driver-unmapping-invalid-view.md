---
title: バグ チェック 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
description: DRIVER_UNMAPPING_INVALID_VIEW のバグ チェックでは、0x000000D7 の値を持ちます。 これは、マップされていないアドレスをマップ解除しようとしてドライバーを示します。
ms.assetid: 68075aa7-f579-49c7-a30a-a21312625ff9
keywords:
- バグ チェック 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
- DRIVER_UNMAPPING_INVALID_VIEW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_UNMAPPING_INVALID_VIEW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0ff8167dae85d03572f73e6c58881cd9b3a10152
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361566"
---
# <a name="bug-check-0xd7-driverunmappinginvalidview"></a>バグ チェック 0xD7:ドライバー\_UNMAPPING\_無効な\_ビュー


ドライバー\_UNMAPPING\_無効な\_ビューのバグ チェックが 0x000000D7 の値を持ちます。 これは、マップされていないアドレスをマップ解除しようとしてドライバーを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="driverunmappinginvalidview-parameters"></a>ドライバー\_UNMAPPING\_無効な\_パラメーターの表示


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
<td align="left"><p>仮想アドレスの割り当てを解除</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>1:</strong>ビューがマップされています。</p>
<p><strong>2:</strong>ビューがコミットされています。</p></td>
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

 

<a name="remarks"></a>注釈
-------

エラーの原因となったドライバーは、スタック トレースから決定できます。

 

 




