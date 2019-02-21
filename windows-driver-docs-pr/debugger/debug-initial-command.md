---
title: 最初のコマンドをデバッグします。
description: 最初のコマンドをデバッグします。
ms.assetid: 0af0b53d-455f-4cdb-b956-9d7e49601733
keywords:
- 最初のコマンド (グローバル フラグ) のデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: db307765b1432f3d435951c59b0f444c018a6e26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529646"
---
# <a name="debug-initial-command"></a>最初のコマンドをデバッグします。


## <span id="ddk_debug_initial_command_dtools"></span><span id="DDK_DEBUG_INITIAL_COMMAND_DTOOLS"></span>


**最初のコマンドをデバッグ**フラグは、クライアント サーバー ランタイム サブシステム (CSRSS) と、WinLogon プロセスをデバッグします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>dic</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x4</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネル フラグ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

プロセスをデバッグする NTSD (コマンドを使用して**ntsd-d**)、コントロールは、カーネル デバッガーにリダイレクトされますが、します。

NTSD について詳しくは、次を参照してください。[デバッグを使用して CDB、NTSD](debugging-using-cdb-and-ntsd.md)します。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[Win32 サブシステムのデバッグを有効にします。](enable-debugging-of-win32-subsystem.md)

 

 





