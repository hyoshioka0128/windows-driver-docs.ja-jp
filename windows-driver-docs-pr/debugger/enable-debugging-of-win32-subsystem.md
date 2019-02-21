---
title: Win32 サブシステムのデバッグを有効にします。
description: Win32 サブシステムのデバッグを有効にします。
ms.assetid: ea9d1c96-413e-42b7-a0c2-b114aa6de2a6
keywords:
- Win32 サブシステム (グローバル フラグ) のデバッグを有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e49aa42cdb795a2eea5acd5241c764ad3521560
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532844"
---
# <a name="enable-debugging-of-win32-subsystem"></a>Win32 サブシステムのデバッグを有効にします。


## <span id="ddk_enable_debugging_of_win32_subsystem_dtools"></span><span id="DDK_ENABLE_DEBUGGING_OF_WIN32_SUBSYSTEM_DTOOLS"></span>


**Win32 サブシステムのデバッグを有効にする**フラグは NTSD デバッガーでのクライアント サーバー ランタイム サブシステム (csrss.exe)、デバッグします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>d32</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x20000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_ENABLE_CSRDEBUG</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

NTSD コマンドを使用して、プロセスをデバッグする**ntsd-d-p-1**します。

このフラグは、有効な場合にのみ、[最初のコマンドをデバッグ](debug-initial-command.md)フラグ (dic) または[デバッグ WinLogon](debug-winlogon.md)フラグ (dwl) も設定されます。

NTSD について詳しくは、次を参照してください。[デバッグを使用して CDB、NTSD](debugging-using-cdb-and-ntsd.md)します。

 

 





