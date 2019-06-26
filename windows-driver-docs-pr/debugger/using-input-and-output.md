---
title: 入力と出力の使用
description: 入力と出力の使用
ms.assetid: 7a23ee09-0314-400a-8152-eef49a225427
keywords:
- デバッガー エンジン、入力と出力
- 入力と出力
- 出力
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56040c8fc5bb4f7c4700f407391e095eec0f249b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366324"
---
# <a name="using-input-and-output"></a>入力と出力の使用


## <span id="ddk_input_and_output_dbx"></span><span id="DDK_INPUT_AND_OUTPUT_DBX"></span>


デバッガー エンジンの入力と出力ストリームの概要については、次を参照してください。[入力と出力](input-and-output.md)します。

### <a name="span-idinputspanspan-idinputspaninput"></a><span id="input"></span><span id="INPUT"></span>入力

エンジンはすべてのクライアントからの入力を求める場合、 [**入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol-input)メソッドは、クライアントで呼び出されます。 呼び出し元の入力が返される**入力**します。

### <a name="span-idinput-callbacksspanspan-idinputcallbacksspaninput-callbacks"></a><span id="input-callbacks"></span><span id="INPUT_CALLBACKS"></span>入力のコールバック

エンジンは、クライアントからの入力が表示されたら、使用して、 [IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)そのクライアント オブジェクトに登録します。 **IDebugInputCallbacks**クライアントを使用したオブジェクトが登録されて[ *SetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)します。 各クライアントには、最大で 1 つを指定できる**IDebugInputCallbacks**登録されるオブジェクト。

入力要求が、エンジンの呼び出し元で始まる、 [ **IDebugInputCallbacks::StartInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebuginputcallbacks-startinput)メソッド。 これにより、 **IDebugInputCallbacks**オブジェクト、エンジンが入力を待機しているようになりました。

場合、 **IDebugInputCallbacks**オブジェクトには、エンジンのいくつかの入力、呼び出すことができます、 [ **ReturnInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-returninput)任意のクライアントのメソッド。 1 回、 **ReturnInput**メソッドが呼び出された、エンジンはこれ以上の入力は実行されません。 このメソッドの後続の呼び出し元には、入力が受信していないことが通知されます。

エンジンを呼び出して[ **IDebugInputCallbacks::EndInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebuginputcallbacks-endinput)を待機中の入力が停止したことを示します。

最後に、エンジンがこの入力に登録済みをエコーするは**IDebugOutputCallbacks** (1 つの入力を指定するために使用) を除くすべてのクライアントのオブジェクトを使用して[ **IDebugOutputCallbacks::Output**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)デバッグ に設定するビット マスクと\_出力\_ダイアログを表示します。

### <a name="span-idoutputspanspan-idoutputspanoutput"></a><span id="output"></span><span id="OUTPUT"></span>出力

エンジンに送信される出力例 - 複数のクライアント メソッドを使用して[*出力*](https://msdn.microsoft.com/library/windows/hardware/ff553183)と[ *OutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputvalist)します。 出力を受信すると、エンジンは、それを一部のクライアントに送信します。

クライアントを使用して、*出力マスク*で関心のある出力の種類を指定します。 出力は、エンジンによって生成される、たびにセレクターがその出力の種類を指定するマスク。 出力の種類には、クライアントの出力のマスクが一致すると、クライアントは、出力を受信します。 呼び出すことによって設定される出力マスク[ **SetOutputMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setoutputmask)を使用して照会および[ **GetOutputMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getoutputmask)します。 参照してください[**デバッグ\_出力\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-output-xxx)出力マスクの値の詳細についてはします。

出力をエンジンを送信するクライアントの一覧がによって制御される、*出力制御*します。 通常、出力の制御はすべてのクライアントに出力を送信する設定します。ただし、一時的に変更できますを使用して[ *ControlledOutput* ](https://msdn.microsoft.com/library/windows/hardware/ff539248)と[ *ControlledOutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-controlledoutputvalist)します。 参照してください[**デバッグ\_OUTCTL\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-outctl-xxx)詳細については、コントロールの値を出力します。

出力は、エンジンによってバッファリングされる場合があります。 出力の複数の部分はエンジンに渡された場合は収集する可能性があり、1 つの大きな部分で、クライアントに送信します。 このバッファーをフラッシュするには使用[ **FlushCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)します。

各クライアント オブジェクトには、*出力幅*、これは、クライアント オブジェクトの出力の表示の幅。 この幅はヒントとして使用のみはいくつかのコマンドと拡張関数の出力をこの幅に基づく書式設定します。 幅は GetOutputWidth メソッドによって返され、SetOutputWidth メソッドを使用して設定できます。

### <a name="span-idoutput-callbacksspanspan-idoutputcallbacksspanoutput-callbacks"></a><span id="output-callbacks"></span><span id="OUTPUT_CALLBACKS"></span>出力のコールバック

使用して、エンジンは、出力をクライアントに送信するときに、 [IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugoutputcallbacks)クライアント オブジェクトに登録します。 **IDebugOutputCallbacks**クライアントを使用したオブジェクトが登録されて[ *SetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)します。 各クライアントには、最大で 1 つを指定できる**IDebugInputCallbacks**登録されるオブジェクト。

出力では、エンジンの呼び出しを送信する、 [ **IDebugOutputCallbacks::Output** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)メソッド。

### <a name="span-idoutput-line-prefixspanspan-idoutputlineprefixspanoutput-line-prefix"></a><span id="output-line-prefix"></span><span id="OUTPUT_LINE_PREFIX"></span>出力行のプレフィックス

各クライアント オブジェクトには、*出力行のプレフィックス*クライアント オブジェクトに関連付けられた出力コールバックに送信される出力のすべての行にこれが付加されます。 これは、インデントを設定または出力の各行の識別のマークを配置に使用できます。

出力行のプレフィックスは GetOutputLinePrefix によって返され、SetOutputLinePrefix を使用して設定できます。 出力行のプレフィックスとをもう一度後で変更を一時的に変更するには、PushOutputLinePrefix と PopOutputLinePrefix を使用します。

### <a name="span-idlog-filesspanspan-idlogfilesspanlog-files"></a><span id="log-files"></span><span id="LOG_FILES"></span>ログ ファイル

デバッガー エンジンでは、デバッグ セッションを記録するログ ファイルを開くことがサポートしています。 最大で一度に 1 つのログ ファイルを開くできます。 出力のコールバックに送信される出力は、(ない場合にログに記録されないフラグが付き) にもこのログ ファイルに送信されます。

ログ ファイルを開くには、次のように使用します。 [ **OpenLogFile2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-openlogfile2) (または[ **OpenLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-openlogfile))。 メソッド[ **GetLogFile2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getlogfile2) (または[ **GetLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getlogfile)) 現在開いているログ ファイルを返します。 ログ ファイルを閉じるには、次のように使用します。 [ **CloseLogFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-closelogfile)します。

メソッド[ **SetLogMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setlogmask) 、ログ ファイルに送信される出力をフィルター処理に使用できると[ **GetLogMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getlogmask)は現在のログ ファイルを返しますフィルターです。

### <a name="span-idpromptspanspan-idpromptspanprompt"></a><span id="prompt"></span><span id="PROMPT"></span>プロンプト

対話型のデバッグ セッションでは、デバッガーがユーザー入力を待機していることをユーザーに示すために、プロンプトを使用できます。 使用して出力のコールバックにメッセージが送信される、 [ *OutputPrompt* ](https://msdn.microsoft.com/library/windows/hardware/ff553227)と[ *OutputPromptVaList* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputpromptvalist)メソッド。 標準のプロンプトの内容がによって返される[ **GetPromptText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getprompttext)します。

 

 





