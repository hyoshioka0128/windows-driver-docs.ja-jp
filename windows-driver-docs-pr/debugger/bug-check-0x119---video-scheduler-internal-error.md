---
title: バグチェック 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
description: VIDEO_SCHEDULER_INTERNAL_ERROR のバグチェックの値は0x00000119 です。 これは、ビデオスケジューラが致命的な違反を検出したことを示します。
ms.assetid: dfffdd70-c519-4e39-a604-a0ba2217093b
keywords:
- バグチェック 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
- VIDEO_SCHEDULER_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_SCHEDULER_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ecc3c1adaeb8f3956a0a5f19c4efb14646a1e1d
ms.sourcegitcommit: 3405003dfd52682948f569253099545d8f9513ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2019
ms.locfileid: "70912720"
---
# <a name="bug-check-0x119-video_scheduler_internal_error"></a>バグ チェック 0x119:ビデオ\_スケジューラ\_の内部\_エラー


ビデオ\_スケジューラ\_の内部\_エラーのバグチェックには、値0x00000119 が含まれています。 これは、ビデオスケジューラが致命的な違反を検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="video_scheduler_internal_error-parameters"></a>ビデオ\_スケジューラ\_の内部\_エラーパラメーター


パラメーター1は目的の唯一のパラメーターであり、正確な違反を識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>ドライバーが無効なフェンス ID を報告しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>コマンドの送信時にドライバーが失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>コマンドバッファーにパッチを適用したときにドライバーが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>ドライバーが無効なフリップ機能を報告しました。</p></td>
</tr>
</tbody>
</table>

 
## <a name="resolution"></a>解決方法

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 

 




