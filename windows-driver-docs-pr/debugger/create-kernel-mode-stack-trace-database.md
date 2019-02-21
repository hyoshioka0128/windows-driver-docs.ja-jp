---
title: カーネル モード スタック トレースのデータベースを作成します。
description: カーネル モード スタック トレースのデータベースを作成します。
ms.assetid: 0c1f94c0-ebc7-4e3c-8101-ba3cf830e7f8
keywords:
- カーネル モード スタック トレース データベース (グローバル フラグ) の作成します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0b92527797d311c111c96a104c3e89100c02892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531412"
---
# <a name="create-kernel-mode-stack-trace-database"></a>カーネル モード スタック トレースのデータベースを作成します。


## <span id="ddk_create_kernel_mode_stack_trace_database_dtools"></span><span id="DDK_CREATE_KERNEL_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


**カーネル モードのスタック トレースのデータベースの作成**フラグはリソース オブジェクトおよびオブジェクトの管理操作などのカーネルの操作の実行時のスタック トレースのデータベースを作成し、Windows のチェック ビルドを使用する場合にだけ機能します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>kst</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x2000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_KERNEL_STACK_TRACE_DB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

GFlags カーネル フラグを設定すると、このフラグを表示しますが、カーネルが既に開始されているために、実行時に、効率的ではありません。

 

 





