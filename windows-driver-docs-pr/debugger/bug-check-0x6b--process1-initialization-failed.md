---
title: バグチェック 0x6B PROCESS1_INITIALIZATION_FAILED
description: PROCESS1_INITIALIZATION_FAILED バグチェックの値は0x0000006B です。 このバグチェックは、Microsoft Windows オペレーティングシステムの初期化に失敗したことを示します。
ms.assetid: 8680d924-3041-4927-a228-52b281bbc267
keywords:
- バグチェック 0x6B PROCESS1_INITIALIZATION_FAILED
- PROCESS1_INITIALIZATION_FAILED
ms.date: 06/27/2018
topic_type:
- apiref
api_name:
- PROCESS1_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8844b140081356f810c6fe10ab3ca2fb266ca992
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534619"
---
# <a name="bug-check-0x6b-process1_initialization_failed"></a>バグチェック 0x6B: PROCESS1 の \_ 初期化に \_ 失敗しました


PROCESS1 の \_ 初期化に \_ 失敗したバグチェックの値は、0x0000006b です。 このバグチェックは、Microsoft Windows オペレーティングシステムの初期化に失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="process1_initialization_failed-parameters"></a>PROCESS1 の \_ 初期化に \_ 失敗したパラメーター


次のパラメーターがブルースクリーンに表示されます。

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
<td align="left"><p>エラーの原因となった NT 状態コード</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
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

ディスクサブシステムのどの部分でも、PROCESS1 の初期化に失敗したバグチェックが発生する可能性があります \_ \_ 。これには、不良ディスク、間違ったケーブル、または正しくないケーブル、異なる ATA タイプのデバイスを同じチェーンに混在させる、またはハードウェアの再生成によって使用できないドライブを含めることができます。

このバグチェックは、ブートパーティションのファイルが見つからないか、[**ドライバー** ] タブでユーザーが誤って無効にしたドライバーによって発生することもあります。

 
## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 




