---
title: Bug Check 0x7D INSTALL_MORE_MEMORY
description: INSTALL_MORE_MEMORY のバグ チェックでは、0x0000007D の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムを起動するには、十分なメモリはないことを示します。
ms.assetid: 560cfa2b-f000-4dc9-8505-f539f3f56fd6
keywords:
- Bug Check 0x7D INSTALL_MORE_MEMORY
- INSTALL_MORE_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INSTALL_MORE_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f0f18a3045be986662710ed768e9e2e482221af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361742"
---
# <a name="bug-check-0x7d-installmorememory"></a>バグ チェック 0x7D:インストール\_詳細\_メモリ


インストール\_詳細\_メモリのバグ チェックが 0x0000007D の値を持ちます。 このバグ チェックでは、Microsoft Windows オペレーティング システムを起動するには、十分なメモリはないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="installmorememory-parameters"></a>インストール\_詳細\_メモリ パラメーター


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
<td align="left"><p>ある物理ページの数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>最下位の物理ページ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>最上位の物理ページ</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows オペレーティング システムには、スタートアップ プロセスを完了するための十分なメモリがありません。

<a name="resolution"></a>解決方法
----------

多くのメモリをインストールします。

 

 




