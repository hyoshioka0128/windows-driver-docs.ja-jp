---
title: バグ チェック 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL のバグ チェックでは、0x000000D5 の値を持ちます。 これは、ドライバーが既に解放されているメモリを参照することを示します。
ms.assetid: b86e55d2-122f-40ac-adb3-092511d3274e
keywords:
- バグ チェック 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
- DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dab6edef93910f19e79bb622794b9bcc6e39d7ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361556"
---
# <a name="bug-check-0xd5-driverpagefaultinfreedspecialpool"></a>バグ チェック 0xD5:ドライバー\_ページ\_フォールト\_IN\_FREED\_特殊\_プール


ドライバー\_ページ\_フォールト\_IN\_FREED\_特殊\_プールのバグ チェックが 0x000000D5 の値を持ちます。 これは、ドライバーが既に解放されているメモリを参照することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="driverpagefaultinfreedspecialpool-parameters"></a>ドライバー\_ページ\_フォールト\_IN\_FREED\_特殊\_プールのパラメーター


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
<td align="left"><p>参照されているメモリ アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>メモリ (わかる場合) を参照されているアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

Driver Verifier**特別なプール**オプションが既に解放されているメモリにアクセスするドライバーをキャッチします。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

<a name="remarks"></a>注釈
-------

これで保護することはできません、 **- お試しくださいを除く**ハンドラー--プローブによってのみ保護できます。

 

 




