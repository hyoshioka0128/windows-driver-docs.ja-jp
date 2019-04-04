---
title: 要求ハンドラー
description: 要求ハンドラー
ms.assetid: bfc543bf-18a8-4e2c-ba7a-d0a21cefb038
keywords:
- I/O キューの作成の WDK KMDF
- 要求ハンドラーの I/O キュー WDK KMDF、
- 要求ハンドラー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d636e10958b2d9254d40bff7dacaf7a7aab872b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551244"
---
# <a name="request-handlers"></a>要求ハンドラー





順次または並列には、ドライバーが指定した場合[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)I/O キューの場合、フレームワーク、ドライバーによって提供されるコールバック関数たびに、キューの要求のいずれかをドライバーに配信する準備ができています。

ドライバーが I/O キューごとと呼ばれる次のコールバック関数の 1 つ以上提供できる*要求ハンドラー*:

<a href="" id="evtioread"></a>[*EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)  
フレームワークの I/O キューの[ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)読み取り要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiowrite"></a>[*EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)  
フレームワークの I/O キューの[ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813)書き込み要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiodevicecontrol"></a>[*EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)  
フレームワークの I/O キューの[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)デバイス I/O 制御の要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiointernaldevicecontrol"></a>[*EvtIoInternalDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541768)  
フレームワークの I/O キューの[ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768)デバイス I/O が内部のコントロール要求は、キューで利用できる場合は、コールバック関数。

<a href="" id="evtiodefault"></a>[*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)  
フレームワークの I/O キューの[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)コールバック関数のすべての要求が使用できるドライバーが関連付けられている要求の種類に固有のコールバック関数を提供していない場合。

呼び出すときに、ドライバーがコールバック関数を登録[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)デバイスの I/O キューを作成します。

これらのコールバック関数の 2 つの入力引数を受信します。 フレームワークは、ドライバーと、要求に保持されている I/O キューを識別するハンドルを提供する I/O 要求を識別するハンドル。 コールバック関数が呼び出すことによって、ターゲット デバイスを調べる[ **WdfIoQueueGetDevice**](https://msdn.microsoft.com/library/windows/hardware/ff547421)します。

フレームワークは、任意のスレッド コンテキストで、ドライバーの要求ハンドラーを呼び出します。 ドライバーを任意のスレッド コンテキストで実行中に長時間待機する必要があります。 場合によってには、ドライバーは、同期メカニズムとしてカーネルのディスパッチャー オブジェクトを使用する可能性があります。 ディスパッチャー オブジェクトの場合、ドライバーが待機できる場合とできない場合の対処方法については、[カーネルのディスパッチャー オブジェクトの概要](https://msdn.microsoft.com/library/windows/hardware/ff548068)を参照してください。

 

 





