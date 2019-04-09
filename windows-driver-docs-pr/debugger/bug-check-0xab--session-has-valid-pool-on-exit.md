---
title: バグ チェック 0xAB SESSION_HAS_VALID_POOL_ON_EXIT
description: SESSION_HAS_VALID_POOL_ON_EXIT のバグ チェックでは、0x000000AB の値を持ちます。 このバグ チェックでは、セッションのアンロードがセッションのドライバーはメモリに保持されているときに発生したことを示します。
ms.assetid: fe4587cc-2567-4452-a3e7-22a53def76b2
keywords:
- バグ チェック 0xAB SESSION_HAS_VALID_POOL_ON_EXIT
- SESSION_HAS_VALID_POOL_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_POOL_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7196d3521573b4b97792400e06901721d3fe9394
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239797"
---
# <a name="bug-check-0xab-sessionhasvalidpoolonexit"></a>バグ チェック 0xAB:セッション\_HAS\_有効\_プール\_ON\_終了


セッション\_HAS\_有効\_プール\_ON\_終了のバグ チェックが 0x000000AB の値を持ちます。 このバグ チェックでは、セッションのアンロードがセッションのドライバーはメモリに保持されているときに発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="sessionhasvalidpoolonexit-parameters"></a>セッション\_HAS\_有効\_プール\_ON\_終了パラメーター


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
<td align="left"><p>セッション id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>リークしているページ プールのバイト数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>リークしている非ページ プールのバイト数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>リークしているページおよび非ページの割り当ての合計数。 (非ページ割り当ての数が、この単語の上半分はおよびページ割り当ては、この単語の下半分で)。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

セッション\_HAS\_有効\_プール\_ON\_セッション ドライバーは、セッションのアンロードの前に割り当てられたプールを解放しないために、終了のバグ チェックが発生します。 このバグ チェックでは、Win32k.sys、Atmfd.dll、Rdpdd.dll、またはビデオやその他のドライバーのバグを指定できます。

 

 




