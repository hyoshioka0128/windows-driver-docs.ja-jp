---
title: コールバック オブジェクトを使用します。
description: コールバック オブジェクトを使用します。
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
ms.openlocfilehash: 02ff9f920b156b9f66374fe084502d78edd79313
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559794"
---
# <a name="using-callback-objects"></a>コールバック オブジェクトを使用します。


これには、エンジンによって使用されるインターフェイスのように 3 つのコールバック COM があります。[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)に通知するため[拡張機能をデバッガー](debugger-extensions.md)エンジンまたはターゲットに変更のアプリケーションと[IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785)要求元の入力と[IDebugOutputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550801)出力を送信するためです。

コールバック オブジェクトは、クライアントで登録されます。 最大で (Unicode および ASCII のバージョンと同じインターフェイスとしてインターフェイスの数) の各クライアントでの各 3 つのコールバック インターフェイスの 1 つのインスタンスを登録できます。

クライアントが作成されたときに、エンジンが作成されたスレッドを記憶します。 コールバック インスタンスがクライアントに登録する呼び出しを実行するたびに、エンジンはこの同じスレッドを使用します。 スレッドが使用中の場合は、キュー、エンジンを実行すると、呼び出しにします。 これらのエンジンを許可するメソッドを呼び出し、 [ *DispatchCallbacks* ](https://msdn.microsoft.com/library/windows/hardware/ff541970)クライアントのスレッドがアイドル状態のときに呼び出す必要があります。 メソッド[ **ExitDispatch** ](https://msdn.microsoft.com/library/windows/hardware/ff543265)により*DispatchCallbacks*を返します。 スレッドが同じスレッドでデバッガー セッションを開始するために使用された場合、エンジンは、中にコールバックの呼び出しを行うことができます、 [ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)メソッドをおよび*DispatchCallbacks*呼び出される必要はありません。

メソッド[ **FlushCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff545475)バッファリングされているすべての出力の出力のコールバックを送信するエンジンに指示します。

### <a name="span-ideventcallbacksspanspan-ideventcallbacksspanevent-callback-objects"></a><span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>イベントのコールバック オブジェクト

[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)インターフェイスは、デバッガーの拡張機能とのアプリケーションに通知する、エンジンによって使用[イベント](events.md#events)と、エンジンとターゲットを変更します。 実装**IDebugEventCallbacks**を使用してクライアントに登録できる[ *SetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556671)します。 使用して、クライアントに登録されている現在の実装を検出できる[ *GetEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff546601)します。 使用して検出できるすべてのクライアントで登録されたイベントのコールバック数[ *GetNumberEventCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547896)します。

エンジンがイベントを管理する方法について詳しくは、[監視イベント](monitoring-events.md)を参照してください。

### <a name="span-idinputcallbacksspanspan-idinputcallbacksspaninput-callback-objects"></a><span id="input_callbacks"></span><span id="INPUT_CALLBACKS"></span>コールバック オブジェクトを入力します。

[IDebugInputCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550785)インターフェイスは、デバッガーの拡張機能とアプリケーションからの入力を要求する、エンジンによって使用されます。 実装**IDebugInputCallbacks**を使用してクライアントに登録できる[ *SetInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556721)します。 使用して、クライアントに登録されている現在の実装を検出できる[ *GetInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff546892)します。 使用して検出できるすべてのクライアントで登録された入力のコールバック数[ *GetNumberInputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547923)します。

エンジンが入力を管理する方法について詳しくは、[入力と出力](using-input-and-output.md)を参照してください。

### <a name="span-idoutputcallbacksspanspan-idoutputcallbacksspanoutput-callback-objects"></a><span id="output_callbacks"></span><span id="OUTPUT_CALLBACKS"></span>コールバック オブジェクトを出力します。

**IDebugOutputCallbacks**インターフェイスは、デバッガーの拡張機能とアプリケーションに出力を送信する、エンジンによって使用されます。 実装**IDebugOutputCallbacks**を使用してクライアントに登録できる[ *SetOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff556751)します。 使用して、クライアントに登録されている現在の実装を検出できる[ *GetOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff548071)します。 使用して検出できるすべてのクライアントで登録されている出力コールバック数[ *GetNumberOutputCallbacks*](https://msdn.microsoft.com/library/windows/hardware/ff547931)します。

エンジンが出力を管理する方法について詳しくは、[入力と出力](using-input-and-output.md)を参照してください。

**注**   、エンジンを呼び出して、COM オブジェクトの一般的なものは、 **iunknown::addref**クライアント、登録されている場合、コールバック COM オブジェクトでと **:release**ときオブジェクトを交換するか、クライアントが削除されます。

 

 

 





