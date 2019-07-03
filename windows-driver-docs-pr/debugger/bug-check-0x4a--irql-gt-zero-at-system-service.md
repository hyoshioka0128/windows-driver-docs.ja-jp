---
title: バグ チェック 0x4A IRQL_GT_ZERO_AT_SYSTEM_SERVICE
description: IRQL_GT_ZERO_AT_SYSTEM_SERVICE のバグ チェックでは、0x0000004A の値を持ちます。 これは、スレッドに返すことユーザー モード システム呼び出しからの IRQL が PASSIVE_LEVEL のまだときを示します。
ms.assetid: 0da64630-d446-426a-a51f-34117fe9daa7
keywords:
- バグ チェック 0x4A IRQL_GT_ZERO_AT_SYSTEM_SERVICE
- IRQL_GT_ZERO_AT_SYSTEM_SERVICE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_GT_ZERO_AT_SYSTEM_SERVICE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 141c75154110429660bc5f1a2a24c6ddd0785bb7
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519415"
---
# <a name="bug-check-0x4a-irqlgtzeroatsystemservice"></a>バグ チェック 0x4A:IRQL\_GT\_0\_で\_システム\_サービス


IRQL\_GT\_0\_で\_システム\_サービスのバグ チェックが 0x0000004A の値を持ちます。 スレッドを返すことをユーザー モードにシステムの呼び出しからの IRQL がパッシブのまだときにこれを示します\_レベル。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="irqlgtzeroatsystemservice-parameters"></a>IRQL\_GT\_0\_で\_システム\_サービス パラメーター


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
<td align="left"><p>システム関数 (呼び出しルーチンのシステム) のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>現在の IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>解決方法 
[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。
 

 




