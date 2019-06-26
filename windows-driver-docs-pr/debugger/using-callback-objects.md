---
title: コールバック オブジェクトの使用
description: コールバック オブジェクトの使用
ms.assetid: 9090a465-b6ab-4e99-8155-b0abdb729468
keywords:
- デバッガー エンジン API、コールバック オブジェクト
- コールバック オブジェクト
- コールバック オブジェクト、イベントのコールバック
- イベントのコールバック
- コールバック オブジェクト、入力のコールバック
- 入力のコールバック
- コールバック オブジェクト、出力のコールバック
- 出力のコールバック
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18c293fff01458b000002857bececceca2e62e8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368629"
---
# <a name="using-callback-objects"></a>コールバック オブジェクトの使用


これには、エンジンによって使用されるインターフェイスのように 3 つのコールバック COM があります。[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)に通知するため[拡張機能をデバッガー](debugger-extensions.md)エンジンまたはターゲットに変更のアプリケーションと[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)要求元の入力と[IDebugOutputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugoutputcallbacks)出力を送信するためです。

コールバック オブジェクトは、クライアントで登録されます。 最大で (Unicode および ASCII のバージョンと同じインターフェイスとしてインターフェイスの数) の各クライアントでの各 3 つのコールバック インターフェイスの 1 つのインスタンスを登録できます。

クライアントが作成されたときに、エンジンが作成されたスレッドを記憶します。 コールバック インスタンスがクライアントに登録する呼び出しを実行するたびに、エンジンはこの同じスレッドを使用します。 スレッドが使用中の場合は、キュー、エンジンを実行すると、呼び出しにします。 これらのエンジンを許可するメソッドを呼び出し、 [ *DispatchCallbacks* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-dispatchcallbacks)クライアントのスレッドがアイドル状態のときに呼び出す必要があります。 メソッド[ **ExitDispatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-exitdispatch)により*DispatchCallbacks*を返します。 スレッドが同じスレッドでデバッガー セッションを開始するために使用された場合、エンジンは、中にコールバックの呼び出しを行うことができます、 [ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドをおよび*DispatchCallbacks*呼び出される必要はありません。

メソッド[ **FlushCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-flushcallbacks)バッファリングされているすべての出力の出力のコールバックを送信するエンジンに指示します。

### <a name="span-ideventcallbacksspanspan-ideventcallbacksspanevent-callback-objects"></a><span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>イベントのコールバック オブジェクト

[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイスは、デバッガーの拡張機能とのアプリケーションに通知する、エンジンによって使用[イベント](events.md#events)と、エンジンとターゲットを変更します。 実装**IDebugEventCallbacks**を使用してクライアントに登録できる[ *SetEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)します。 使用して、クライアントに登録されている現在の実装を検出できる[ *GetEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-geteventcallbacks)します。 使用して検出できるすべてのクライアントで登録されたイベントのコールバック数[ *GetNumberEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumbereventcallbacks)します。

エンジンがイベントを管理する方法について詳しくは、次を参照してください。[監視イベント](monitoring-events.md)します。

### <a name="span-idinputcallbacksspanspan-idinputcallbacksspaninput-callback-objects"></a><span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>コールバック オブジェクトを入力します。

[IDebugInputCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebuginputcallbacks)インターフェイスは、デバッガーの拡張機能とアプリケーションからの入力を要求する、エンジンによって使用されます。 実装**IDebugInputCallbacks**を使用してクライアントに登録できる[ *SetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setinputcallbacks)します。 使用して、クライアントに登録されている現在の実装を検出できる[ *GetInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getinputcallbacks)します。 使用して検出できるすべてのクライアントで登録された入力のコールバック数[ *GetNumberInputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumberinputcallbacks)します。

エンジンが入力を管理する方法について詳しくは、次を参照してください。[入力と出力](using-input-and-output.md)します。

### <a name="span-idoutputcallbacksspanspan-idoutputcallbacksspanoutput-callback-objects"></a><span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>コールバック オブジェクトを出力します。

**IDebugOutputCallbacks**インターフェイスは、デバッガーの拡張機能とアプリケーションに出力を送信する、エンジンによって使用されます。 実装**IDebugOutputCallbacks**を使用してクライアントに登録できる[ *SetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setoutputcallbacks)します。 使用して、クライアントに登録されている現在の実装を検出できる[ *GetOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getoutputcallbacks)します。 使用して検出できるすべてのクライアントで登録されている出力コールバック数[ *GetNumberOutputCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumberoutputcallbacks)します。

エンジンが出力を管理する方法について詳しくは、次を参照してください。[入力と出力](using-input-and-output.md)します。

**注**   、エンジンを呼び出して、COM オブジェクトの一般的なものは、 **iunknown::addref**クライアント、登録されている場合、コールバック COM オブジェクトでと **:release**ときオブジェクトを交換するか、クライアントが削除されます。

 

 

 





