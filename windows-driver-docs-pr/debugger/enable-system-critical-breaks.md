---
title: システムの重要な区切りを有効にします。
description: システムの重要な区切りを有効にします。
ms.assetid: f13372b9-604e-4ea5-96e2-d8b7e916c8e5
keywords:
- システムの重要な改 (グローバル フラグ) を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c6da80674db36165f0ac1fac4333b43d72c489
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560217"
---
# <a name="enable-system-critical-breaks"></a>システムの重要な区切りを有効にします。


## <span id="ddk_enable_system_critical_breaks_dtools"></span><span id="DDK_ENABLE_SYSTEM_CRITICAL_BREAKS_DTOOLS"></span>


**システムの重要な区切りを有効にする**フラグがデバッガーにシステム区切りを強制します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>scb</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x100000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_ENABLE_SYSTEM_CRIT_BREAKS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>変換先</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

プロセス (イメージ ファイル) を設定する場合、このフラグは、システムの中断をデバッガーに、指定されたプロセスが異常停止した場合にします。 このフラグは有効なプロセスを呼び出すときにのみ、 **RtlSetProcessBreakOnExit**と**RtlSetThreadBreakOnExit**インターフェイス。

システム全体を設定すると (レジストリまたはカーネル フラグ) このフラグは、システムの中断、デバッガーをプロセスがあるたびと呼ばれる、 **RtlSetProcessBreakOnExit**と**RtlSetThreadBreakOnExit**インターフェイスが異常停止します。

 

 





