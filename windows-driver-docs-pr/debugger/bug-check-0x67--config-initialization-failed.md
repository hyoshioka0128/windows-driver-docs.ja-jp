---
title: Bug Check 0x67 CONFIG_INITIALIZATION_FAILED
description: CONFIG_INITIALIZATION_FAILED のバグ チェックでは、0x00000067 の値を持ちます。 このバグ チェックでは、レジストリ構成が失敗したことを示します。
ms.assetid: 3bc4d6d9-785e-4283-b4c5-2c868c03f084
keywords:
- Bug Check 0x67 CONFIG_INITIALIZATION_FAILED
- CONFIG_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CONFIG_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 586b07c5223b81ec3ba04e4ea3b4fe386662d606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539575"
---
# <a name="bug-check-0x67-configinitializationfailed"></a>バグ チェック 0x67 の。CONFIG\_初期化\_失敗


CONFIG\_初期化\_失敗のバグ チェックが 0x00000067 の値を持ちます。 このバグ チェックでは、レジストリ構成が失敗したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="configinitializationfailed-parameters"></a>CONFIG\_初期化\_FAILED パラメーター


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
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>場所の選択</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>NT 状態コード</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

レジストリは、必要なレジストリ ファイルを格納するプールを割り当てられませんでした。 多数のページ プールが使用できるように、登録の早い段階でシステムの初期化には、このプールが割り当てられるため、このような状況は発生しません。

 

 




