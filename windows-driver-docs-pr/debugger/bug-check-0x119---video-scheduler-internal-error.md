---
title: バグ チェック 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
description: VIDEO_SCHEDULER_INTERNAL_ERROR のバグ チェックでは、0x00000119 の値を持ちます。 これは、ビデオのスケジューラで致命的な違反が検出されたことを示します。
ms.assetid: dfffdd70-c519-4e39-a604-a0ba2217093b
keywords:
- バグ チェック 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
- VIDEO_SCHEDULER_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_SCHEDULER_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1702af363ee3049d518b5d08a172abe5efed48ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358165"
---
# <a name="bug-check-0x119-videoschedulerinternalerror"></a>バグ チェック 0x119:ビデオ\_スケジューラ\_内部\_エラー


ビデオ\_スケジューラ\_内部\_エラーのバグ チェックが 0x00000119 の値を持ちます。 これは、ビデオのスケジューラで致命的な違反が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="videoschedulerinternalerror-parameters"></a>ビデオ\_スケジューラ\_内部\_エラー パラメーター


パラメーター 1 では、関心のある唯一のパラメーターは、し、正確な違反を識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>無効なフェンス ID、ドライバーから報告されました</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ドライバーは、コマンドの送信時に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>コマンド バッファー修正プログラムの適用時に、ドライバーが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>ドライバーには、無効なの反転機能が報告されました。</p></td>
</tr>
</tbody>
</table>

 

 

 




