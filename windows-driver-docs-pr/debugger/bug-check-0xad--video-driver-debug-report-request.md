---
title: バグ チェック 0xAD VIDEO_DRIVER_DEBUG_REPORT_REQUEST
description: VIDEO_DRIVER_DEBUG_REPORT_REQUEST のバグ チェックでは、0x000000AD の値を持ちます。 このバグ チェックでは、ビデオ ポートに、実行時に、ビデオ ドライバーの代わりの致命的でないミニダンプが作成されたことを示します。
ms.assetid: eedde484-584b-478b-9429-a9c78bb62c1e
keywords:
- バグ チェック 0xAD VIDEO_DRIVER_DEBUG_REPORT_REQUEST
- VIDEO_DRIVER_DEBUG_REPORT_REQUEST
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DRIVER_DEBUG_REPORT_REQUEST
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52d850961d7b0707c94659ac36716e63958af794
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557852"
---
# <a name="bug-check-0xad-videodriverdebugreportrequest"></a>バグ チェック 0xAD の。ビデオ\_ドライバー\_デバッグ\_レポート\_要求


ビデオ\_ドライバー\_デバッグ\_レポート\_バグ チェックが 0x000000AD の値を要求します。 このバグ チェックでは、ビデオ ポートに、実行時に、ビデオ ドライバーの代わりの致命的でないミニダンプが作成されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="videodriverdebugreportrequest-parameters"></a>ビデオ\_ドライバー\_デバッグ\_レポート\_要求パラメーター


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
<td align="left"><p>ドライバー固有</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ドライバー固有</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ドライバー固有</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ブート時間以降に要求されているすべてのレポートの数</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ビデオ ポートは、ビデオ ドライバーがデバッグ レポートを要求したので、実行時に、ビデオ ドライバーの代わりの致命的でないミニダンプを作成します。

ビデオ\_ドライバー\_デバッグ\_レポート\_バグ チェックは、完全なダンプまたはカーネル ダンプの作成ではなく、ミニダンプの作成によってのみ発生することを要求します。

 

 




