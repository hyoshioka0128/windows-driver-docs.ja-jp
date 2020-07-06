---
title: .scriptdebug (JavaScript のデバッグ)
description: . Scriptdebug コマンドを使用して、JavaScript スクリプトをデバッグします。
keywords:
- . scriptdebug デバッグ JavaScript Windows デバッグ
ms.date: 12/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .scriptdebug (Debug JavaScript)
api_type:
- NA
ms.openlocfilehash: 43a503f3c5f2891a13bc35228aea2f8a93ff668f
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968038"
---
# <a name="scriptdebug-debug-javascript"></a>.scriptdebug (JavaScript のデバッグ)

**. Scriptdebug**コマンドを使用して、JavaScript スクリプトをデバッグします。

```dbgcmd
.scriptdebug FileName
```

### <a name="parameters"></a>パラメーター

*FileName*

デバッグするデバッガー JavaScript スクリプトの名前を指定します。

### <a name="span-idenvironmentspanenvironment"></a><span id="Environment"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>



## <a name="span-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span>追加情報

JavaScript のデバッグの概要については、「 [Javascript デバッガースクリプト-Javascript デバッグ](javascript-debugger-scripting.md#DEBUGGING)」を参照してください。

>[!NOTE] 
> WinDbg Preview で JavaScript のデバッグを使用するには、管理者としてデバッガーを実行します。
>


<a name="remarks"></a>注釈
-------

JavaScript をデバッグする前に、次の手順を完了しました。

1. [**読み込み (拡張 DLL の読み込み)**](-load---loadby--load-extension-dll-.md)コマンドを使用して、JavaScript スクリプトプロバイダーを読み込みます。 

    ```dbgcmd
    0:000> .load jsprovider.dll
    ```

2. サンプルスクリプトを読み込みます。

    ```dbgcmd
    0:000> .scriptload C:\MyScripts\DebuggableSample.js
    ```

スクリプトのアクティブデバッグを開始するには、 **scriptdebug**コマンドを使用します。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

プロンプトが表示されたら *>>> Debug [DebuggableSample <No Position> ] >* と入力の要求が、スクリプトデバッガーの内部にあります。  

**Help**コマンドまたは **?** JavaScript デバッグ環境にコマンドの一覧を表示します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >.help
Script Debugger Commands (*NOTE* IDs are **PER SCRIPT**):
    ? .................................. Get help
    ? <expr>  .......................... Evaluate expression <expr> and display result
    ?? <expr>  ......................... Evaluate expression <expr> and display result
    |  ................................. List available scripts
    |<scriptid>s  ...................... Switch context to the given script
    bc <bpid>  ......................... Clear breakpoint by specified <bpid>
    bd <bpid>  ......................... Disable breakpoint by specified <bpid>
    be <bpid>  ......................... Enable breakpoint by specified <bpid>
    bl  ................................ List breakpoints
    bp <line>:<column>  ................ Set breakpoint at the specified line and column
    bp <function-name>  ................ Set breakpoint at the (global) function specified by the given name
    bpc  ............................... Set breakpoint at current location
    dv  ................................ Display local variables of current frame
    g  ................................. Continue script
    gu   ............................... Step out
    k  ................................. Get stack trace
    p  ................................. Step over
    q  ................................. Exit script debugger (resume execution)
    sx  ................................ Display available events/exceptions to break on
    sxe <event>  ....................... Enable break on <event>
    sxd <event>  ....................... Disable break on <event>
    t  ................................. Step in
    .attach <scriptId>  ................ Attach debugger to the script specified by <scriptId>
    .detach [<scriptId>]  .............. Detach debugger from the script specified by <scriptId>
    .frame <index>  .................... Switch to frame number <index>
    .f+  ............................... Switch to next stack frame
    .f-  ............................... Switch to previous stack frame
    .help  ............................. Get help
```


### <a name="events"></a>イベント

**Sx**スクリプトデバッガーコマンドを使用して、トラップできるイベントの一覧を表示します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

**Sxe**スクリプトデバッガーコマンドを使用して、中断動作を有効にします。 たとえば、スクリプトが実行されるコードが実行されるとすぐにスクリプトデバッガーにトラップされるように、エントリのブレークをオンにするには、次のコマンドを使用します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```

**Sxd**スクリプトデバッガーコマンドを使用して、ブレークポイントの動作を無効にします。

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

### <a name="stack-trace"></a>スタック トレース

スタックトレースを表示するには、 **k**コマンドを使用します。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

### <a name="enumerating-variables"></a>変数の列挙

使用**する方法** JavaScript 変数の値を列挙する場合は。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >??someObj                
??someObj                                                   
someObj          : {...}                                    
    __proto__        : {...}                                
    a                : 0x63                                 
    b                : {...}                                
```


### <a name="breakpoints"></a>ブレークポイント

追加のブレークポイントを操作するには、次のブレークポイントコマンドを使用します。


**bp <bpid> **: ブレークポイントの設定

**bd <bpid> **: ブレークポイントを無効にします

**be <bpid> **: ブレークポイントを有効にする

**bc <bpid> **: ブレークポイントのクリア

**bpc**: 現在の行にブレークポイントを設定します

**bl**: ブレークポイントの一覧表示


### <a name="flow-control---navigation"></a>フロー制御-ナビゲーション

次のコマンドを使用して、スクリプト内を前方に移動します。

**p**: ステップオーバー

**t**: ステップイン

**g**: スクリプトの続行

**gu**: ステップアウト




### <a name="frames"></a>連結

次のコマンドを使用して、フレームを操作します。


**. frame <index> **: フレーム番号に切り替えます<index>

**. f +**: 次のスタックフレームに切り替えます

**. f +**: 前のスタックフレームに切り替えます


### <a name="quiting"></a>Quiting

**デタッチ**コマンドを使用して、JavaScript デバッガーをデタッチします。 

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

**Q**コマンドを使用して JavaScript デバッガーを終了します。 

```dbgcmd
>>> Debug [<NONE> ] >q                                      
q                                                           
```

