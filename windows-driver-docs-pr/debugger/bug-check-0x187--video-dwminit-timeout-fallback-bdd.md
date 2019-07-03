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
ms.openlocfilehash: bd250c5652827c17dde8f02fc9724ba4310f716e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519870"
---
# <a name="bug-check-0x187-videodwminittimeoutfallbackbdd"></a>バグ チェック 0x187:ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD


ビデオ\_DWMINIT\_タイムアウト\_フォールバック\_BDD のバグ チェックが 0x00000187 の値を持ちます。 これは、そのビデオは IHV ドライバーを使用するのではなく、BDD に戻りましたを示します。 これにより、ライブのダンプが常に生成されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


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

 

 

 




