---
title: バグ チェック 0x187 VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
description: VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD のバグ チェックでは、0x00000187 の値を持ちます。 これは、そのビデオは IHV ドライバーを使用するのではなく、BDD に戻りましたを示します。 これにより、ライブのダンプが常に生成されます。
ms.assetid: CF4AB5DB-2779-4E6E-BF27-AE320403A982
keywords:
- バグ チェック 0x187 VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
- VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DWMINIT_TIMEOUT_FALLBACK_BDD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7e0dfb2fa7b58048f72081cdf9d13c1945d4f97c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581098"
---
# <a name="bug-check-0x187-videodwminittimeoutfallbackbdd"></a>バグ チェック 0x187:ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD


ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD のバグ チェックが 0x00000187 の値を持ちます。 これは、そのビデオは IHV ドライバーを使用するのではなく、BDD に戻りましたを示します。 これにより、ライブのダンプが常に生成されます。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="videodwminittimeoutfallbackbdd-parameters"></a>ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD パラメーター


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
<td align="left">理由コード。
<p>0x1:DWM は、後の再試行、"stopping"ディスプレイ アダプター、および BDD にフォールバックを初期化できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">予約済み</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">予約済み</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




