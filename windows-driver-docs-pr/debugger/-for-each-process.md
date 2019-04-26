---
title: for_each_process
description: For_each_process 拡張機能は、ターゲット内プロセスごとに 1 回指定されているデバッガー コマンドを実行します。
ms.assetid: 28cc0982-43a4-41ba-a26f-6910cc1b77b8
keywords:
- Windows デバッグ for_each_process
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 593fe189f633221301386a25b8fa5987d542c008
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336672"
---
# <a name="foreachprocess"></a>! の\_各\_プロセス


**! の\_各\_プロセス**拡張機能は、ターゲット内プロセスごとに 1 回指定されているデバッガー コマンドを実行します。

```dbgcmd
!for_each_process ["CommandString"] 
!for_each_process -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
プロセスごとに実行するデバッガー コマンドを指定します。

場合*クラスヒント*複数のコマンドが含まれていますセミコロン (;) で区切ります。囲みます*クラスヒント*引用符 (")。 場合*クラスヒント*、内の個々 のコマンドである引用符で囲まれた*クラスヒント*引用符を含めることはできません。 内で*クラスヒント*、  **@\#プロセス**プロセスのアドレスが置き換えられます。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

この拡張機能は、Ext.dll に存在する場合でも、カーネル モードでのみ動作します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

プロセスの概要については、次を参照してください。[スレッドとプロセス](controlling-threads-and-processes.md)します。 操作またはプロセスに関する情報を取得する方法については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>注釈
-------

引数が指定されていない場合、デバッガーには、時間と優先順位の統計情報とともに、すべてのプロセスの一覧が表示されます。 これは入力に相当[ **! @ プロセス\#プロセス 0** ](-process.md)として、*クラスヒント*値。

任意の時点での実行を終了するには、(WinDbg) では、CTRL + BREAK または (KD) では、CTRL + C キーを押します。

 

 





