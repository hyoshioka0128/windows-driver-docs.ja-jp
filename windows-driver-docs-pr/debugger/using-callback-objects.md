---
title: コールバック オブジェクトの使用
description: コールバック オブジェクトの使用
ms.assetid: 9090a465-b6ab-4e99-8155-b0abdb729468
keywords:
- デバッガーエンジン API, コールバックオブジェクト
- コールバックオブジェクト
- コールバックオブジェクト、イベントコールバック
- イベントコールバック
- コールバックオブジェクト、入力コールバック
- 入力コールバック
- コールバックオブジェクト、出力コールバック
- 出力コールバック
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7592c8fdf79fc4f85a22a6e1b92d6d15a13c515
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834251"
---
# <a name="using-callback-objects"></a>コールバック オブジェクトの使用


エンジンによって使用されるコールバック COM インターフェイスには、 [IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)によってエンジンまたはターゲットに対する変更[の通知、](debugger-extensions.md)入力要求の[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks) 、出力を送信するための[IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugoutputcallbacks) 。

コールバックオブジェクトは、クライアントに登録されます。 最大で、3つのコールバックインターフェイスの1つのインスタンスを各クライアントに登録できます (同じインターフェイスとして、インターフェイス数の Unicode および ASCII バージョン)。

クライアントが作成されると、エンジンは、作成されたスレッドを記憶します。 エンジンは、クライアントに登録されているコールバックインスタンスを呼び出すたびに、この同じスレッドを使用します。 スレッドが使用中の場合、エンジンは、必要な呼び出しをキューに置いています。 エンジンがこれらの呼び出しを実行できるようにするには、クライアントのスレッドがアイドル状態になるたびに、メソッド[*DispatchCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-dispatchcallbacks)を呼び出す必要があります。 [**Exitdispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-exitdispatch)メソッドによって、 *DispatchCallbacks*が返されます。 スレッドが、デバッガーセッションを開始するために使用されたスレッドと同じである場合、エンジンは[**Waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッド中にコールバック呼び出しを行うことができ、 *DispatchCallbacks*を呼び出す必要はありません。

メソッド[**Flushcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)は、バッファリングされたすべての出力を出力コールバックに送信するようにエンジンに指示します。

### <a name="span-idevent_callbacksspanspan-idevent_callbacksspanevent-callback-objects"></a><span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>イベントコールバックオブジェクト

エンジンは、 [IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイスを使用して、[イベント](events.md#events)およびエンジンとターゲットへの変更をデバッガーに通知します。 **IDebugEventCallbacks**の実装は、 [*seteventcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)を使用してクライアントに登録できます。 クライアントに登録されている現在の実装は、 [*Geteventcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-geteventcallbacks)を使用して見つけることができます。 すべてのクライアントに対して登録されているイベントコールバックの数は、 [*Getnumber Eventコールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumbereventcallbacks)を使用して検出できます。

エンジンがイベントを管理する方法の詳細については、「[イベントの監視](monitoring-events.md)」を参照してください。

### <a name="span-idinput_callbacksspanspan-idinput_callbacksspaninput-callback-objects"></a><span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>入力コールバックオブジェクト

[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebuginputcallbacks)インターフェイスは、デバッガーの拡張機能とアプリケーションからの入力を要求するためにエンジンによって使用されます。 **IDebugInputCallbacks**の実装は、 [*setinputcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)を使用してクライアントに登録できます。 クライアントに登録されている現在の実装は、 [*Getinputcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getinputcallbacks)を使用して見つけることができます。 すべてのクライアントに対して登録されている入力コールバックの数は、 [*Getnumber Inputコールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumberinputcallbacks)を使用して見つけることができます。

エンジンが入力を管理する方法の詳細については、「[入力と出力](using-input-and-output.md)」を参照してください。

### <a name="span-idoutput_callbacksspanspan-idoutput_callbacksspanoutput-callback-objects"></a><span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>出力コールバックオブジェクト

**IDebugOutputCallbacks**インターフェイスは、デバッガーの拡張機能とアプリケーションに出力を送信するためにエンジンによって使用されます。 **IDebugOutputCallbacks**の実装は、 [*setoutputcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)を使用してクライアントに登録できます。 クライアントに登録されている現在の実装は、 [*Getoutputcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getoutputcallbacks)を使用して見つけることができます。 すべてのクライアントに対して登録されている出力コールバックの数は、 [*Getnumber Outputコールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumberoutputcallbacks)を使用して見つけることができます。

エンジンが出力を管理する方法の詳細については、「[入力と出力](using-input-and-output.md)」を参照してください。

**注**   COM オブジェクトの場合と同様に、エンジンは、コールバック COM オブジェクトがクライアントに登録されている場合は、そのオブジェクトに対して**Iunknown:: AddRef**を呼び出し、オブジェクトが置換されるか、クライアントが削除されるときに**iunknown:: Release**を呼び出します。

 

 

 





