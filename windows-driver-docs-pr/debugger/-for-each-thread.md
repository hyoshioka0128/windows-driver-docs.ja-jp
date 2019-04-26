---
title: for_each_thread
description: For_each_thread 拡張機能は、ターゲットで、スレッドごとに 1 回指定されているデバッガー コマンドを実行します。
ms.assetid: 4ca8e1bd-1a1b-4fef-a2d9-42c26f9b746b
keywords:
- Windows デバッグ for_each_thread
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27874f8e518ebe33cd20de0cda693f63b90f3478
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336643"
---
# <a name="foreachthread"></a>! の\_各\_スレッド


**! の\_各\_スレッド**拡張機能は、ターゲットの各スレッドに対して 1 回指定されているデバッガー コマンドを実行します。

```dbgcmd
!for_each_thread ["CommandString"] 
!for_each_thread -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
各スレッドに実行するデバッガー コマンドを指定します。 場合*クラスヒント*複数のコマンドが含まれていますセミコロン (;) で区切ります。囲みます*クラスヒント*引用符 (")。 場合*クラスヒント*、内の個々 のコマンドである引用符で囲まれた*クラスヒント*引用符を含めることはできません。 内で*クラスヒント*、  **@\#スレッド**スレッド アドレスが置き換えられます。

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

スレッドの概要については、次を参照してください。[スレッドとプロセス](controlling-threads-and-processes.md)します。 操作またはスレッドに関する情報の取得の詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>注釈
-------

引数が指定されていない場合、デバッガーは、すべてのスレッドの一覧を表示します。、スレッドと状態を待機します。 これは入力に相当[ **! @ スレッド\#スレッド 2** ](-process.md)として、*クラスヒント*値。

CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C を押して任意の時点での実行を終了できます。

 

 





