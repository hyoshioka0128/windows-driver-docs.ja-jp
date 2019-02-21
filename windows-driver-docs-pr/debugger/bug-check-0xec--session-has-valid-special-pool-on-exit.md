---
title: バグ チェック 0 xec です SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
description: SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT のバグ チェックでは、0x000000EC の値を持ちます。 これは、セッションのアンロードがセッションのドライバーはメモリに保持されているときに発生したことを示します。
ms.assetid: 0100684b-cde6-4f15-93da-78d200fa2f80
keywords:
- バグ チェック 0 xec です SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
- SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_SPECIAL_POOL_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 162ae0a011b5bd196172cacedf22d407ba6d9613
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553749"
---
# <a name="bug-check-0xec-sessionhasvalidspecialpoolonexit"></a>バグのチェック 0 xec です。セッション\_HAS\_有効\_特殊\_プール\_ON\_終了


セッション\_HAS\_有効\_特殊\_プール\_ON\_終了のバグ チェックが 0x000000EC の値を持ちます。 これは、セッションのアンロードがセッションのドライバーはメモリに保持されているときに発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="sessionhasvalidspecialpoolonexit-parameters"></a>セッション\_HAS\_有効\_特殊\_プール\_ON\_終了パラメーター


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
<td align="left"><p>セッション ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>リークしている特別なプール ページの数</p></td>
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

 

<a name="cause"></a>原因
-----

このエラーは、セッションのアンロードの前に、特別なプールの割り当てを解放していないセッション ドライバーで発生します。 これは、win32k.sys、atmfd.dll、rdpdd.dll、またはビデオ ドライバーのバグを示します。

 

 




