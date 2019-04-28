---
title: Debug WinLogon
description: Debug WinLogon
ms.assetid: c30e6b83-685a-4e4e-88bf-1e05776ac87a
keywords:
- WinLogon (グローバル フラグ) のデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef49034e95e55e3f1a8aa55c69a8172759eb7a47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368156"
---
# <a name="debug-winlogon"></a>Debug WinLogon


## <span id="ddk_debug_winlogon_dtools"></span><span id="DDK_DEBUG_WINLOGON_DTOOLS"></span>


**デバッグ WinLogon**フラグは、WinLogon サービスをデバッグします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>dwl</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND_EX</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Winlogon プロセスをデバッグする NTSD (コマンドを使用して**ntsd-d-g-x**)、コントロールは、カーネル デバッガーにリダイレクトされますが、します。

NTSD について詳しくは、次を参照してください。[デバッグを使用して CDB、NTSD](debugging-using-cdb-and-ntsd.md)します。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>参照してください。

[最初のコマンドをデバッグ](debug-initial-command.md)、 [Win32 サブシステムのデバッグを有効にします。](enable-debugging-of-win32-subsystem.md)

 

 





