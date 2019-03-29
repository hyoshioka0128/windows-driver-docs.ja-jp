---
title: Stop on exception
description: Stop on exception
ms.assetid: f459fa28-2fdf-4094-ba58-7e01a2309bb7
keywords:
- 例外 (グローバル フラグ) の停止します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b79223fdaa80d7417e82089e8449ddb63b5bf546
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579395"
---
# <a name="stop-on-exception"></a>Stop on exception


## <span id="ddk_stop_on_exception_dtools"></span><span id="DDK_STOP_ON_EXCEPTION_DTOOLS"></span>


**例外で停止**フラグによって、カーネルをカーネル モードの例外が発生するたびに、カーネル デバッガーを中断します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>soe と略記されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_STOP_ON_EXCEPTION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Windows は、最初にすべての例外を渡します (状態を除く\_ポート\_切断)、ローカルの例外ハンドラーに渡す前にデバッガーに警告やエラーの重大度レベル。

 

 





