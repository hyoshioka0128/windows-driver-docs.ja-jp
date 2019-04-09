---
title: バグ チェック 0x11C ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
description: ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE のバグ チェックでは、configuration manager の保護されたストレージに書き込みが試行されたことを示す 0x0000011C の値を持ちます。
ms.assetid: 5a322457-51d7-4832-8eeb-1fdc99f313e8
keywords:
- バグ チェック 0x11C ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
- ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f81d0527f891851e6ecb0530e09515c7d860809b
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239727"
---
# <a name="bug-check-0x11c-attemptedwritetocmprotectedstorage"></a>バグ チェック 0x11C:試行\_書き込み\_TO\_CM\_PROTECTED\_ストレージ


試行\_書き込み\_TO\_CM\_PROTECTED\_記憶域のバグ チェックが 0x0000011C の値を持ちます。 このバグ チェックでは、configuration manager の読み取り専用の保護されたストレージに書き込むしようとすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="attemptedwritetocmprotectedstorage-parameters"></a>試行\_書き込み\_TO\_CM\_PROTECTED\_ストレージ パラメーター


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
<td align="left"><p>書き込みの試行は、仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>PTE 内容</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

可能ですが、バグの Unicode 文字列画面を確認し、KiBugCheckDriver に保存し、書き込み操作を試行しているドライバーの名前が出力されます。

 

 




