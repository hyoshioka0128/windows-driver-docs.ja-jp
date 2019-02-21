---
title: .scriptdebug (デバッグ JavaScript)
description: JavaScript スクリプトをデバッグするのにには、.scriptdebug コマンドを使用します。
keywords:
- .scriptdebug デバッグの JavaScript Windows デバッグ
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
ms.openlocfilehash: cd1dd7119b2eca9716e7b4779319c37b538e62cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535455"
---
# <a name="scriptdebug-debug-javascript"></a>.scriptdebug (デバッグ JavaScript)

使用して、 **.scriptdebug** JavaScript スクリプトをデバッグするコマンド。

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



## <a name="span-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span>追加情報

JavaScript のデバッグの概要については、次を参照してください。 [JavaScript デバッガーのスクリプティング - JavaScript のデバッグ](javascript-debugger-scripting.md#DEBUGGING)します。

>[!NOTE] 
> WinDbg のプレビューでは、JavaScript のデバッグを使用するには、管理者として、デバッガーを実行します。
>


<a name="remarks"></a>注釈
-------

前に、デバッグ、JavaScript は、次の手順を完了します。

1. 使用して JavaScript スクリプト プロバイダーを読み込み、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)コマンド。 

    ```dbgcmd
    0:000> .load jsprovider.dll
    ```

2. サンプル スクリプトを読み込みます。

    ```dbgcmd
    0:000> .scriptload C:\MyScripts\DebuggableSample.js
    ```

スクリプトの使用状況を積極的にデバッグを開始する、 **.scriptdebug**コマンド。

```dbgcmd
0:000> .scriptdebug C:\MyScripts\DebuggableSample.js
>>> ****** DEBUGGER ENTRY DebuggableSample ******
           No active debug event!

>>> Debug [DebuggableSample <No Position>] >
```

プロンプトが表示されたら *>>> デバッグ [DebuggableSample <No Position>] >* スクリプト デバッガー内では入力を要求します。  

使用して、 **.help**コマンドまたは**でしょうか。** JavaScript のデバッグ環境では、コマンドの一覧を表示します。

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

使用して、 **sx**トラップできるはイベントの一覧を表示するデバッガー コマンドのスクリプトを作成します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sx              
sx                                                          
    ab  [   inactive] .... Break on script abort            
    eh  [   inactive] .... Break on any thrown exception    
    en  [   inactive] .... Break on entry to the script     
    uh  [     active] .... Break on unhandled exception     
```

使用して、 **sxe**デバッガー コマンドを中断動作を有効にするスクリプトを作成します。 内の任意のコードを実行するとすぐにスクリプト デバッガーに、スクリプトをトラップするためのエントリをブレークをオンにする例では、このコマンドを使用します。

```dbgcmd
>>> Debug [DebuggableSample <No Position>] >sxe en          
sxe en                                                      
Event filter 'en' is now active                             
```

使用して、 **sxd**デバッガーのブレークポイントの動作を無効にするコマンドのスクリプトを作成します。

```dbgcmd                                                                                                                      
>>> Debug [DebuggableSample 34:5] >sxd en                                                                              
sxd en                                                                                                                 
Event filter 'en' is now inactive                                                                                      
```

### <a name="stack-trace"></a>スタック トレース

使用して、 **k**スタック トレースを表示するコマンド。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >k                                                  
k                                                                                     
    ##  Function                         Pos    Source Snippet                        
-> [00] throwAndCatch                    034:05 (var curProc = host.currentProcess)   
   [01] outer                            066:05 (var foo = throwAndCatch())           
   [02] outermost                        074:05 (var result = outer())                
```

### <a name="enumerating-variables"></a>変数を列挙します。

使用 **??** JavaScript の変数の値を列挙します。

```dbgcmd
>>> Debug [DebuggableSample 34:5] >??someObj                
??someObj                                                   
someObj          : {...}                                    
    __proto__        : {...}                                
    a                : 0x63                                 
    b                : {...}                                
```


### <a name="breakpoints"></a>ブレークポイント

追加のブレークポイントを使用するには、次のブレークポイントのコマンドを使用します。


|           |                                |
|-----------|--------------------------------|
| bp <bpid> |        ブレークポイントを設定します。        |
| bd <bpid> |     ブレークポイントを無効にします。     |
| be <bpid> |     ブレークポイントを有効にします。      |
| ビジネス継続性 <bpid> |      ブレークポイントをクリアします。      |
|    bpc    | 現在の行にブレークポイントの設定 |
|    bl     |     ブレークポイントを一覧表示します。     |

### <a name="flow-control---navigation"></a>ナビゲーションのフロー制御

次のコマンドを使用して、スクリプト内を前方に移動します。

|   |                           |
|---|---------------------------|
|p  | ステップ オーバー                 |
|t  | ステップ イン                   |
|g  | スクリプトを続行します。           |
|gu | ステップ アウト                  |



### <a name="frames"></a>フレーム

フレームを使用するには、次のコマンドを使用します。


|                |                                |
|----------------|--------------------------------|
| .frame <index> | フレーム番号に切り替える <index> |
|      .f +       |   次にスタック フレームに切り替え   |
|      .f +       | 前のスタック フレームに切り替える |

### <a name="quiting"></a>容量が増えます

使用して、 **.detach** JavaScript デバッガーをデタッチ コマンド。 

```dbgcmd
>>> Debug [DebuggableSample 34:5] >.detach                  
.detach                                                     
Debugger has been detached from script!                     
```

使用して、 **q** JavaScript デバッガーを終了するコマンド。 

```dbgcmd
>>> Debug [<NONE> ] >q                                      
q                                                           
```

