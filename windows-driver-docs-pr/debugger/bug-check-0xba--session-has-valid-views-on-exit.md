---
title: バグ チェック 0xBA SESSION_HAS_VALID_VIEWS_ON_EXIT
description: SESSION_HAS_VALID_VIEWS_ON_EXIT のバグ チェックでは、0x000000BA の値を持ちます。 セッションのドライバーもがマップされているビュー、セッションのアンロード時にこれを示します。
ms.assetid: e0ef7d0e-8a3e-41ca-b0c1-c0f0bb298ef1
keywords:
- バグ チェック 0xBA SESSION_HAS_VALID_VIEWS_ON_EXIT
- SESSION_HAS_VALID_VIEWS_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_VIEWS_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7d03978c160e718f788db79c5b8ad85d74b3004b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361640"
---
# <a name="bug-check-0xba-sessionhasvalidviewsonexit"></a>バグ チェック 0xBA:セッション\_HAS\_有効\_ビュー\_ON\_終了


セッション\_HAS\_有効\_ビュー\_ON\_終了のバグ チェックが 0x000000BA の値を持ちます。 セッションのドライバーもがマップされているビュー、セッションのアンロード時にこれを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="sessionhasvalidviewsonexit-parameters"></a>セッション\_HAS\_有効\_ビュー\_ON\_終了パラメーター


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
<td align="left"><p>リークしているマップのビューの数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>このセッションのマップ ビューのテーブルのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>このセッションのマップ ビューのテーブルのサイズ</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このエラーは、セッションのアンロードの前に、マップ ビューのマッピング解除しないセッション ドライバーによって発生します。 これは、win32k.sys、atmfd.dll、rdpdd.dll、またはビデオ ドライバーのバグを示します。

 

 




