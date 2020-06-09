---
title: バグチェック 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
description: DRIVER_UNMAPPING_INVALID_VIEW バグチェックの値は0x000000D7 です。 これは、ドライバーが、マップされていないアドレスのマッピングを解除しようとしていることを示します。
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
ms.openlocfilehash: c69a4233e26bbeca5d5d52141b2b92c29331f7cb
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534541"
---
# <a name="bug-check-0xd7-driver_unmapping_invalid_view"></a>バグチェック 0xD7: \_ \_ 無効なビューのマップ解除 \_


無効なビューのマップを解除すると、 \_ \_ \_ バグチェックの値が0x000000D7 になります。 これは、ドライバーが、マップされていないアドレスのマッピングを解除しようとしていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_unmapping_invalid_view-parameters"></a>\_ \_ 無効な \_ ビューパラメーターのマッピングを解除したドライバー


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

 

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 [ [**Kb (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) ] コマンドを使用してスタックトレースを取得します。エラーの原因となったドライバーは、スタックトレースから特定できます。

 

 




