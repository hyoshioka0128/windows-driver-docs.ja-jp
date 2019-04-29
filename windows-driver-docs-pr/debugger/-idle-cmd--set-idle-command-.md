---
title: .idle_cmd (アイドル コマンドの設定)
description: .Idle_cmd コマンドでは、アイドル状態のコマンドを設定します。 これは、デバッガーに、ターゲットから制御が戻りますたびに実行されるコマンドです。
ms.assetid: 8cfe7aa8-4e31-4e97-b61d-9e8bb1b7be61
keywords:
- .idle_cmd (アイドル状態コマンドのセット) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .idle_cmd (Set Idle Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 551d784cf4e1ed7c18aa6cb9ef36bcdd7937743b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336471"
---
# <a name="idlecmd-set-idle-command"></a>.idle\_cmd (アイドル状態のコマンドの設定)


**.Idle\_cmd**コマンドのセット、*コマンドをアイドル*します。 これは、デバッガーに、ターゲットから制御が戻りますたびに実行されるコマンドです。 たとえば、ターゲットでは、ブレークポイントに達すると、このコマンドを実行します。

```dbgcmd
.idle_cmd
.idle_cmd String 
.idle_cmd /d
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *文字列*   
アイドル状態のコマンドを設定する必要があります、文字列を指定します。

<span id="________d______"></span><span id="________D______"></span> **/d**   
アイドル状態のコマンドをクリアします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、スクリプト ファイルでは使用できません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ときに **.idle\_cmd**使用は、パラメーターなしのアイドル状態の現在のコマンドが表示されます。

、WinDbg でアイドル状態のコマンドは、ワークスペースに格納されます。

次に例を示します。 設定されているアイドル状態のコマンドは、 [ **r eax**](r--registers-.md)します。 次に、デバッガーがアイドル状態で既にため、このコマンドすぐに実行します、表示、 **eax**登録します。

```dbgcmd
windbg> .idle_cmd r eax 
Execute when idle: r eax
eax=003b0de8
```

 

 





