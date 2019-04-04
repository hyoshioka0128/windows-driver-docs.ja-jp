---
title: .remote_exit (exit クライアントのデバッグ)
description: .Remote_exit コマンドでは、デバッグ、クライアントが終了したが、デバッグ セッションは終了しません。
ms.assetid: 9e15a842-6864-4ff9-97bc-f6cc8549a422
keywords:
- デバッグ クライアント (.remote_exit) コマンドを終了します。
- リモート デバッグ、デバッガーでは、終了デバッグ クライアント (.remote_exit) コマンド
- .remote_exit (デバッグ クライアントを終了する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .remote_exit (Exit Debugging Client)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f19ade2702be6d8b1df22fbe6444458a77fbb3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550148"
---
# <a name="remoteexit-exit-debugging-client"></a>.remote\_exit (終了デバッグ クライアント)


**.Remote\_終了**コマンドは、デバッグのクライアントを終了しますが、デバッグ セッションは終了しません。

```dbgcmd
.remote_exit [FinalCommands]
```

## <a name="span-idddkmetaexitdebuggingclientdbgspanspan-idddkmetaexitdebuggingclientdbgspanparameters"></a><span id="ddk_meta_exit_debugging_client_dbg"></span><span id="DDK_META_EXIT_DEBUGGING_CLIENT_DBG"></span>パラメーター


<span id="_______FinalCommands______"></span><span id="_______finalcommands______"></span><span id="_______FINALCOMMANDS______"></span> *FinalCommands*   
デバッグ サーバーに渡すコマンド文字列を指定します。 セミコロンを使用して、複数のコマンドを分離する必要があります。 これらのコマンドは、デバッグのサーバーに渡され、接続が切断されます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

使用することができます、 **.remote\_終了**コマンドをスクリプト ファイルにのみ存在します。 KD、CDB で使用することができますが、WinDbg で使用することはできません。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スクリプト ファイルの詳細については、[スクリプト ファイルを使用する](using-script-files.md)を参照してください。 クライアントをデバッグおよびサーバーのデバッグに関する詳細については、[リモート デバッグで、デバッガー](remote-debugging-through-the-debugger.md)を参照してください。

<a name="remarks"></a>注釈
-------

使用して、デバッグのクライアントを終了することができる場合、直接使用するか、KD、CDB、スクリプトを使用してではなく、 [ **CTRL + B** ](ctrl-b--quit-local-debugger-.md)キー。

WinDbg で実行されるスクリプトを使用してデバッグするクライアントを終了することはできません。

 

 





