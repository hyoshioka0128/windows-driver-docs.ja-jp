---
title: バグ チェック 0x10F RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
description: RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED のバグ チェックでは、0x0000010F の値を持ちます。
ms.assetid: d2589163-8c82-4416-a378-a0c72360a9fb
keywords:
- バグ チェック 0x10F RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
- RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8bec499ee149adf1499175b867d8e8cda28b45ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367933"
---
# <a name="bug-check-0x10f-resourcemanagerexceptionnothandled"></a>バグ チェック 0x10F:リソース\_MANAGER\_例外\_いない\_処理済み


リソース\_MANAGER\_例外\_いない\_処理済みのバグ チェックが 0x0000010F の値を持ちます。 これは、カーネル トランザクション マネージャーには、カーネル モードのリソース マネージャーが直接コールバックへの応答での例外を発生したことが検出されたことを示します。 リソース マネージャーは、予期しないと、回復不能な状態では。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="resourcemanagerexceptionnothandled-parameters"></a>リソース\_MANAGER\_例外\_いない\_処理済みのパラメーター


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
<td align="left"><p>例外レコードのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>コンテキスト レコードのアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>例外コードのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>リソース マネージャーのアドレス</p></td>
</tr>
</tbody>
</table>

 

 

 




