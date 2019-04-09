---
title: Bug Check 0x51 REGISTRY_ERROR
description: REGISTRY_ERROR のバグ チェックでは、0x00000051 の値を持ちます。 これは、レジストリの重大なエラーが発生したことを示します。
ms.assetid: 286e462f-e4d4-408f-91ad-3e20336e2025
keywords:
- Bug Check 0x51 REGISTRY_ERROR
- REGISTRY_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f2fe3f647e69f03cbce14c0d0e3376d22e939d9
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238388"
---
# <a name="bug-check-0x51-registryerror"></a>バグ チェック 0x51:レジストリ\_エラー


レジストリ\_エラーのバグ チェックが 0x00000051 の値を持ちます。 これは、レジストリの重大なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="registryerror-parameters"></a>レジストリ\_エラー パラメーター


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
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>(該当する場合)、ハイブへのポインター</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>場合は、hive の破損、リターン コードの<strong>HvCheckHive</strong> (該当する場合)</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

何かは、レジストリの問題が発生しました。 カーネル デバッガーを使用できる場合は、スタック トレースを取得します。

このエラーは、レジストリをいずれかのファイルを読み取るときに I/O エラーが発生したことを示している可能性があります。 これは、ハードウェアの問題またはファイル システムの破損によって発生することができます。

セキュリティ システムでのみ使用される、更新操作に失敗したためにも発生し、しが発生したのみリソースを制限するとします。

 

 




