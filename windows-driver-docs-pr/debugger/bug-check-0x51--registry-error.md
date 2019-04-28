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
ms.openlocfilehash: 990877a9d7f1fc69e24de6ef7cf9cec115750cbf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363544"
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

何かは、レジストリの問題が発生しました。 カーネル デバッガーを使用できる場合は、スタック トレースを取得: [ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)デバッグ拡張機能を根本原因を突き止めるに非常に役立ち、入力のいずれかのことができますとバグ チェックに関する情報を表示します[ **k (Display Stack Backtrace)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)呼び出し履歴を表示するコマンド。

このエラーは、レジストリをいずれかのファイルを読み取るときに I/O エラーが発生したことを示している可能性があります。 これは、ハードウェアの問題またはファイル システムの破損によって発生することができます。

セキュリティ システムでのみ使用される、更新操作に失敗したためにも発生し、しが発生したのみリソースを制限するとします。

 

 




