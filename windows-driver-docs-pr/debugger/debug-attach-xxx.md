---
title: デバッグ\_\_XXX にアタッチ
description: このトピックで説明する DEBUG\_ATTACH\_*XXX*ビットフラグは、デバッガーエンジンがユーザーモードプロセスにアタッチする方法を制御します。
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
ms.openlocfilehash: de54d41b7b4fcd9f0616097ec3b088a192f4fcb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837795"
---
# <a name="debug_attach_xxx"></a>デバッグ\_\_XXX にアタッチ

このトピックで説明する DEBUG\_ATTACH\_*XXX*ビットフラグは、デバッガーエンジンがユーザーモードプロセスにアタッチする方法を制御します。 カーネルターゲットにアタッチするときに使用される DEBUG_ATTACH_XXX オプションについては、 [IDebugClient:: AttachKernel メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient-attachkernel)を参照してください。

指定できる値は次のとおりです。

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
<p>ターゲット noninvasively にアタッチします。  Noninvasive デバッグの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-" data-raw-source="[Noninvasive Debugging (User Mode)](https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-)">Noninvasive デバッグ (ユーザーモード)</a>」を参照してください。</p>
<p>このフラグが設定されている場合は、フラグ DEBUG_ATTACH_EXISTING、DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK、および DEBUG_ATTACH_INVASIVE_RESUME_PROCESS を設定することはできません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_EXISTING"></a><a id="debug_attach_existing"></a><dl>
<dt><b>DEBUG_ATTACH_EXISTING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>デバッガーが既にアタッチされている (または破棄されている可能性があります) アプリケーションに再アタッチします。  ターゲットへの再アタッチの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-" data-raw-source="[.attach (Attach to Process)](https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-)">. attach (プロセスにアタッチ)</a>」を参照してください。</p>
<p>このフラグが設定されている場合は、他の DEBUG_ATTACH_<i>XXX</i>フラグを設定することはできません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND"></a><a id="debug_attach_noninvasive_no_suspend"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>Noninvasively をアタッチするときに、ターゲットのスレッドを一時停止しないでください。</p>
<p>このフラグが設定されている場合は、フラグ DEBUG_ATTACH_NONINVASIVE も設定する必要があります。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK"></a><a id="debug_attach_invasive_no_initial_break"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>ターゲットにアタッチするときに最初のブレークインを要求しないでください。</p>
<p>このフラグが設定されている場合は、フラグ DEBUG_ATTACH_NONINVASIVE と DEBUG_ATTACH_EXISTING を設定することはできません。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_RESUME_PROCESS"></a><a id="debug_attach_invasive_resume_process"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_RESUME_PROCESS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>Invasively をアタッチするときに、すべてのターゲットのスレッドを再開します。</p>
<p>このフラグが設定されている場合は、フラグ DEBUG_ATTACH_NONINVASIVE と DEBUG_ATTACH_EXISTING を設定することはできません。</p>
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
<td align="left">DbgEng .h (DbgEng .h を含む)</td>
</tr>
</tbody>
</table>

 

 





