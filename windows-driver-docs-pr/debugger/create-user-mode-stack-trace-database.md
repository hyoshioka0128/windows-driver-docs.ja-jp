---
title: Create user mode stack trace database
description: Create user mode stack trace database
ms.assetid: c24a42d3-cb06-4ce5-bf90-c8a224bf7d01
keywords:
- ユーザー モードのスタック トレースのデータベース (グローバル フラグ) の作成します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef1a02a450709a125727fe32f3ffa2f1625e650
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374981"
---
# <a name="create-user-mode-stack-trace-database"></a>Create user mode stack trace database


## <span id="ddk_create_user_mode_stack_trace_database_dtools"></span><span id="DDK_CREATE_USER_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


**ユーザー モードのスタック トレースのデータベースの作成**フラグは、特定のプロセス (イメージ ファイルのモード) またはすべてのプロセス (システム全体) のアドレス空間で、ランタイム スタック トレース データベースを作成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>ust</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x1000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_USER_STACK_TRACE_DB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

 

 





