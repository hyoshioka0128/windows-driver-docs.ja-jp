---
title: デバッグ\_アタッチ\_XXX
description: デバッグ\_アタッチ\_*XXX*ビット フラグでは、このトピックで説明されているが、デバッガー エンジンがユーザー モード プロセスにアタッチする方法を制御します。
ms.date: 08/10/2018
topic_type:
- apiref
api_name:
- DEBUG_ATTACH_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 6af76c54acb0e4d55b1ade9ed5849f26706b33f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550819"
---
# <a name="debugattachxxx"></a>デバッグ\_アタッチ\_XXX

デバッグ\_アタッチ\_*XXX*ビット フラグでは、このトピックで説明されているが、デバッガー エンジンがユーザー モード プロセスにアタッチする方法を制御します。 DEBUG_ATTACH_XXX ときに使用されるオプションへのカーネルのターゲットを参照してください、 [IDebugClient::AttachKernel メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient-attachkernel)します。

使用可能な値は、次に示します。

<table>
<tr>
<th>定数</th>
<th>説明</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE"></a><a id="debug_attach_noninvasive"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>Noninvasively ターゲットに接続します。  待合室デバッグの詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-" data-raw-source="[Noninvasive Debugging (User Mode)](https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-)">待合室 (ユーザー モード) のデバッグ</a>します。</p>
<p>このフラグを設定すると、DEBUG_ATTACH_EXISTING、DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK、および DEBUG_ATTACH_INVASIVE_RESUME_PROCESS フラグを設定しない必要があります。 場合、</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_EXISTING"></a><a id="debug_attach_existing"></a><dl>
<dt><b>DEBUG_ATTACH_EXISTING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>アプリケーションをデバッガーが既にアタッチされている (および破棄された可能性があります) に再アタッチします。  ターゲットに再アタッチの詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-" data-raw-source="[.attach (Attach to Process)](https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-)">.attach (プロセスにアタッチ)</a>します。</p>
<p>このフラグがセットを他の DEBUG_ATTACH_ 場合<i>XXX</i>フラグを設定する必要があります。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND"></a><a id="debug_attach_noninvasive_no_suspend"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ターゲットを中断しないように&#39;s スレッド noninvasively にアタッチするときにします。</p>
<p>このフラグが設定されている場合、フラグ DEBUG_ATTACH_NONINVASIVE する必要があります設定することもできます。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK"></a><a id="debug_attach_invasive_no_initial_break"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ターゲットにアタッチするときに、初期の侵入を要求しません。</p>
<p>このフラグが設定されている場合、DEBUG_ATTACH_NONINVASIVE と DEBUG_ATTACH_EXISTING フラグする必要がありますを設定できません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_RESUME_PROCESS"></a><a id="debug_attach_invasive_resume_process"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_RESUME_PROCESS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>すべての対象を再開&#39;s スレッド invasively にアタッチするときにします。</p>
<p>このフラグが設定されている場合、DEBUG_ATTACH_NONINVASIVE と DEBUG_ATTACH_EXISTING フラグする必要がありますを設定できません。</p>
</td>
</tr>
</table>


<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>

 

 





