---
title: for_each_frame
description: For_each_frame 拡張機能は、現在のスレッドのスタックのフレームごとに 1 回のデバッガー コマンドを実行します。
ms.assetid: 7294dc5e-190f-486f-9079-1fb28d6d484b
keywords:
- Windows デバッグ for_each_frame
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_frame
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dbf39c37a8a8ecd090f5afd111f9f1980c1c116d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336663"
---
# <a name="foreachframe"></a>! の\_各\_フレーム


**! の\_各\_フレーム**拡張機能は、現在のスレッドのスタックのデバッガー コマンド フレームごとに 1 回を実行します。

```dbgcmd
!for_each_frame ["CommandString"] 
!for_each_frame -?
```

## <a name="span-idddkforeachframedbgspanspan-idddkforeachframedbgspanparameters"></a><span id="ddk__for_each_frame_dbg"></span><span id="DDK__FOR_EACH_FRAME_DBG"></span>パラメーター


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
各フレームで 1 回実行するデバッガー コマンドを指定します。 場合*クラスヒント*複数のコマンドが含まれていますをセミコロンで区切るしで囲む必要があります*クラスヒント*引用符で囲んで指定します。 各コマンドの中で複数のコマンドを含める場合*クラスヒント*引用符を含めることはできません。 現在のフレーム内のインデックスを参照する*クラスヒント*、@$ フレームの pseudoregister を使用します。

<span id="_______-_______"></span> **-?**   
この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

ローカル コンテキストの詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

<a name="remarks"></a>注釈
-------

任意の引数を指定しない場合、 **! の\_各\_フレーム**拡張機能は、すべてのフレームとそのフレーム インデックスの一覧を表示します。 すべてのフレームの詳細についてを使用して、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

[ **K** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドには、最大で 256 台のフレームがについて説明します。 列挙された各フレームでは、そのフレームが一時的にローカルの現在のコンテキスト (のような[ **.frame (ローカル コンテキストの設定)** ](-frame--set-local-context-.md)コマンド)。 コンテキストが設定されたら、*クラスヒント*を実行します。 ローカル コンテキストをする前にしていた値にリセットがすべてのフレームを使用すると、使用、 **! の\_各\_フレーム**拡張機能。

含める場合*クラスヒント*デバッガーには、フレームが表示されます。 および、そのフレームが実行されたコマンドの前にそのインデックス。

次のコマンドでは、現在のスタックのすべてのローカル変数が表示されます。

```dbgcmd
!for_each_frame !for_each_local dt @#Local
```

 

 





