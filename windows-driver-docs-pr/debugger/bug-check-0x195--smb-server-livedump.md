---
title: バグ チェック 0x195 SMB_SERVER_LIVEDUMP
description: SMB_SERVER_LIVEDUMP のバグ チェックでは、0x00000195 の値を持ちます。 これには、SMB サーバーを選択し、問題を検出しましたがデバッグ情報を収集するカーネル ダンプをキャプチャしたことを示します。
ms.assetid: 302BA6E0-DC7C-4AE7-BD4D-C6F6A74D82D9
keywords:
- バグ チェック 0x195 SMB_SERVER_LIVEDUMP
- SMB_SERVER_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SMB_SERVER_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ede59b825c1413ac59ce8c3baaab97a82eb37bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362064"
---
# <a name="bug-check-0x195-smbserverlivedump"></a>バグ チェック 0x195:SMB\_SERVER\_LIVEDUMP


SMB\_SERVER\_LIVEDUMP バグ チェックが 0x00000195 の値を持ちます。 これには、SMB サーバーを選択し、問題を検出しましたがデバッグ情報を収集するカーネル ダンプをキャプチャしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="smbserverlivedump-parameters"></a>SMB\_SERVER\_LIVEDUMP パラメーター


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
<td align="left"><p>0x1:I/O は、一定の時間で完了できませんでした。</p>
2-ポインター、i/O の SRV2_WORK_ITEM</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
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

 

 

 




