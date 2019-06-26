---
title: バグ チェック 0x190 WIN32K_CRITICAL_FAILURE_LIVEDUMP
description: WIN32K_CRITICAL_FAILURE_LIVEDUMP のバグ チェックでは、0x00000190 の値を持ちます。 これは、Win32k の重大なエラーが発生したことを示します。 デバッグ情報を収集するライブのダンプがキャプチャされます。
ms.assetid: 39C0145D-08FE-4BBC-A729-9E70198CF87F
keywords:
- バグ チェック 0x190 WIN32K_CRITICAL_FAILURE_LIVEDUMP
- WIN32K_CRITICAL_FAILURE_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_CRITICAL_FAILURE_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e336b8bfe76368b730b91ac57e1cec1192079d6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362065"
---
# <a name="bug-check-0x190-win32kcriticalfailurelivedump"></a>バグ チェック 0x190:WIN32K\_重大\_エラー\_LIVEDUMP


WIN32K\_重大\_エラー\_LIVEDUMP バグ チェックが 0x00000190 の値を持ちます。 これは、Win32k の重大なエラーが発生したことを示します。 デバッグ情報を収集するライブのダンプがキャプチャされます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="win32kcriticalfailurelivedump-parameters"></a>WIN32K\_重大\_エラー\_LIVEDUMP パラメーター


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
<td align="left">1</td>
<td align="left"><p>エラーの種類</p>
<p>0x1:REGION_VALIDATION_FAILURE - リージョンは、画面の範囲外です。</p>
2 - DC 3 - 画面 4 ポインター リージョンへのポインターへのポインター
<p>0x2:OPERATOR_NEW_USED -"new"演算子は、メモリの割り当てに使用されます。</p>
2 - 3 - 予約済み 4 - 予約済みの予約</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>

 

 

 




