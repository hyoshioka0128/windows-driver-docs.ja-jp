---
title: so (カーネル デバッグ オプションの設定)
description: コマンドを設定またはカーネル デバッグ オプションを表示するようにします。
ms.assetid: b40260c7-6e60-4198-988f-bcafecb165bc
keywords:
- (セット カーネル デバッグ オプション) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- so (Set Kernel Debugging Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 331c83819a53e818e1dfb962224b3e6583025d05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368108"
---
# <a name="so-set-kernel-debugging-options"></a>so (カーネル デバッグ オプションの設定)


**ように**コマンドを設定またはカーネル デバッグ オプションが表示されます。

```dbgcmd
so [Options] 
```

## <a name="span-idddkcmdsetkerneldebuggingoptionsdbgspanspan-idddkcmdsetkerneldebuggingoptionsdbgspanparameters"></a><span id="ddk_cmd_set_kernel_debugging_options_dbg"></span><span id="DDK_CMD_SET_KERNEL_DEBUGGING_OPTIONS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
1 つまたは複数の次のオプション:

<span id="NOEXTWARNING"></span><span id="noextwarning"></span>**NOEXTWARNING**  
デバッガーは、拡張機能のコマンドを見つけられないときに警告を発行しません。

<span id="NOVERSIONCHECK"></span><span id="noversioncheck"></span>**NOVERSIONCHECK**  
デバッガーの拡張 Dll のバージョンをチェックしません。

省略した場合*オプション*、現在のオプションが表示されます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

カーネル デバッグを使用してオプションを設定することも、 \_NT\_デバッグ\_オプション[環境変数](kernel-mode-environment-variables.md)します。

 

 





