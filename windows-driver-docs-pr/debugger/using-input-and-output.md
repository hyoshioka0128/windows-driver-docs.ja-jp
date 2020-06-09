---
title: 入力と出力の使用
description: 入力と出力の使用
ms.assetid: 7a23ee09-0314-400a-8152-eef49a225427
keywords:
- デバッガーエンジン、入出力
- 入力と出力
- 出力
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37e695f7f9c6bd47f27857bb4f62cd22f98926c5
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534755"
---
# <a name="using-input-and-output"></a>入力と出力の使用


## <span id="ddk_input_and_output_dbx"></span><span id="DDK_INPUT_AND_OUTPUT_DBX"></span>


デバッガーエンジンでの入力ストリームと出力ストリームの概要については、「[入力と出力](input-and-output.md)」を参照してください。

### <a name="span-idinputspanspan-idinputspaninput"></a><span id="input"></span><span id="INPUT"></span>代入

[**入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol-input)方式がクライアントで呼び出された場合、エンジンはすべてのクライアントからの入力を要求します。 入力は、**入力**の呼び出し元に返されます。

### <a name="span-idinput-callbacksspanspan-idinput_callbacksspaninput-callbacks"></a><span id="input-callbacks"></span><span id="INPUT_CALLBACKS"></span>入力コールバック

エンジンは、クライアントからの入力を要求すると、そのクライアントに登録されている[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks)オブジェクトを使用します。 **IDebugInputCallbacks**オブジェクトは、 [*setinputcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)を使用してクライアントに登録できます。 各クライアントには、1つの**IDebugInputCallbacks**オブジェクトを登録できます。

入力の要求は、 [**IDebugInputCallbacks:: StartInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebuginputcallbacks-startinput)メソッドを呼び出すエンジンによって開始されます。 これにより、 **IDebugInputCallbacks**オブジェクトに、エンジンが入力を待機していることが通知されます。

**IDebugInputCallbacks**オブジェクトにエンジンの入力がある場合は、任意のクライアントの[**returninput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-returninput)メソッドを呼び出すことができます。 **Returninput**メソッドが呼び出されると、エンジンはそれ以上入力を行いません。 このメソッドの後続の呼び出し元には、入力が受信されなかったことが通知されます。

次に、エンジンは[**IDebugInputCallbacks:: EndInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebuginputcallbacks-endinput)を呼び出して、入力の待機を停止したことを示します。

最後に、エンジンは、 [**IDebugOutputCallbacks:: output**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)と、デバッグ出力プロンプトに設定されたビットマスクを使用して、この入力をすべてのクライアントの登録済み**IDebugOutputCallbacks**オブジェクトにエコー \_ し \_ ます。

### <a name="span-idoutputspanspan-idoutputspanoutput"></a><span id="output"></span><span id="OUTPUT"></span>出力

出力は、[*出力*](https://msdn.microsoft.com/library/windows/hardware/ff553183)や[*OutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputvalist)など、いくつかのクライアントメソッドを使用してエンジンに送信できます。 出力を受け取ると、エンジンはそれをいくつかのクライアントに送信します。

クライアントは、*出力マスク*を使用して、目的の出力の種類を示します。 エンジンによって出力が生成されるたびに、出力の種類を指定するマスクが付随します。 出力の種類がクライアントの出力マスクと一致する場合、クライアントは出力を受け取ります。 出力マスクは、 [**Setoutputmask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setoutputmask)を呼び出し、 [**getoutputmask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getoutputmask)を使用してクエリを行うことによって設定できます。 出力マスクの値の詳細については、「[**デバッグ \_ 出力 \_ XXX**](debug-output-xxx.md) 」を参照してください。

エンジンが出力を送信するクライアントの一覧は、*出力コントロール*によって制御されます。 通常、出力コントロールは、すべてのクライアントに出力を送信するように設定されています。ただし、 [*ControlControlledOutputVaList output*](https://msdn.microsoft.com/library/windows/hardware/ff539248)と[*ControlledOutputVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-controlledoutputvalist)を使用して一時的に変更することができます。 出力制御値の詳細については、「 [**DEBUG \_ outctl \_ XXX**](debug-outctl-xxx.md) 」を参照してください。

エンジンによって出力がバッファリングされる場合があります。 複数の出力がエンジンに渡されると、それらを収集して、1つの大きな部分でクライアントに送信する場合があります。 このバッファーをフラッシュするには、 [**Flushcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)を使用します。

各クライアントオブジェクトには、クライアントオブジェクトの出力表示の幅である*出力幅*があります。 この幅はヒントとしてのみ使用されますが、一部のコマンドおよび拡張関数は、この幅に基づいて出力を書式設定します。 幅は GetOutputWidth メソッドによって返され、SetOutputWidth メソッドを使用して設定できます。

### <a name="span-idoutput-callbacksspanspan-idoutput_callbacksspanoutput-callbacks"></a><span id="output-callbacks"></span><span id="OUTPUT_CALLBACKS"></span>出力コールバック

エンジンは、クライアントに出力を送信するときに、クライアントに登録されている[IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugoutputcallbacks)オブジェクトを使用します。 [*Setoutputcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)を使用して、 **IDebugOutputCallbacks**オブジェクトをクライアントに登録できます。 各クライアントには、1つの**IDebugInputCallbacks**オブジェクトを登録できます。

出力を送信するために、エンジンは[**IDebugOutputCallbacks:: output**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugoutputcallbacks-output)メソッドを呼び出します。

### <a name="span-idoutput-line-prefixspanspan-idoutput_line_prefixspanoutput-line-prefix"></a><span id="output-line-prefix"></span><span id="OUTPUT_LINE_PREFIX"></span>出力行のプレフィックス

各クライアントオブジェクトには、クライアントオブジェクトに関連付けられた出力コールバックに送信される出力のすべての行に付加された*出力行プレフィックス*があります。 これは、インデントを設定したり、出力の各行に特定のマークを配置したりするために使用できます。

出力行のプレフィックスは GetOutputLinePrefix によって返され、SetOutputLinePrefix を使用して設定できます。 出力行のプレフィックスを一時的に変更し、後で再び変更するには、PushOutputLinePrefix と PopOutputLinePrefix を使用します。

### <a name="span-idlog-filesspanspan-idlog_filesspanlog-files"></a><span id="log-files"></span><span id="LOG_FILES"></span>ログファイル

デバッガーエンジンは、デバッグセッションを記録するログファイルを開くことをサポートしています。 最大で1つのログファイルを同時に開くことができます。 出力コールバックに送信される出力は、このログファイルにも送信されます (ログに記録されないようにフラグが設定されている場合を除く)。

ログファイルを開くには、 [**OpenLogFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-openlogfile2) (または[**openlogfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-openlogfile)) を使用します。 [**GetLogFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getlogfile2) (または[**getlogfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getlogfile)) メソッドは、現在開いているログファイルを返します。 ログファイルを閉じるには、 [**Closelogfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-closelogfile)を使用します。

[**Setlogmask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setlogmask)メソッドを使用して、ログファイルに送信される出力をフィルター処理できます。 [**getlogmask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getlogmask)は、現在のログファイルフィルターを返します。

### <a name="span-idpromptspanspan-idpromptspanprompt"></a><span id="prompt"></span><span id="PROMPT"></span>プロンプト

対話型デバッグセッションでは、プロンプトを使用して、デバッガーがユーザー入力を待機していることをユーザーに示すことができます。 プロンプトは、 [*Outputprompt*](https://msdn.microsoft.com/library/windows/hardware/ff553227)メソッドと[*OutputPromptVaList*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputpromptvalist)メソッドを使用して出力コールバックに送信されます。 標準プロンプトの内容は、 [**Getprompttext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getprompttext)によって返されます。

 

 





