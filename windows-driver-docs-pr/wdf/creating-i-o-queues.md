---
title: I/O キューの作成
description: I/O キューの作成
ms.assetid: 03b09c94-6b72-4234-b21f-203f93b7a2e8
keywords:
- I/O キューの作成の WDK KMDF
- WDK KMDF、既定の I/O キュー
- 既定の I/O キュー WDK KMDF
- WDK KMDF キューの I/O を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2776e77f2310145ad304a87481ac55b0b86fc89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578414"
---
# <a name="creating-io-queues"></a>I/O キューの作成





ほとんどのドライバーでの I/O キューの作成、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 ドライバーをデバイスの I/O キューを作成するには、するには、呼び出しのフレームワークのキュー オブジェクトの[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)メソッド (これは、framework のキュー オブジェクトが作成されます)。 ドライバーの提供、 [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)メソッドに構造体。 この構造体には、キューのなど、キューに関する構成情報が含まれています[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)へのポインターと[要求ハンドラー](request-handlers.md)要求をで使用可能なときにフレームワーク。キューです。 構造体もキューが必要かどうかを示す[電源管理対象](using-power-managed-i-o-queues.md)とキューの I/O 要求に、ドライバーが長さ 0 のバッファーをサポートするかどうか。

ドライバーが設定されている場合、 **DefaultQueue**のメンバー、 [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)構造体を**TRUE**、キューが、デバイスの*既定の I/O キュー*します。 ドライバーは、既定の I/O キューを作成する場合、フレームワークすべてのデバイスの I/O 要求キューに配置この、一部の要求を受信するキューを作成しない限り、します。 ドライバーは呼び出すことによって、デバイスの既定の I/O キューを識別するハンドルを取得することができます、 [ **WdfDeviceGetDefaultQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff545965)メソッド。

デバイスは、複数の I/O キューを使用する場合、ドライバーを呼び出すことができます[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)必要がある多くの queue オブジェクトを作成します。 呼び出すことができる場合、ドライバーは、複数のキューを作成、 [ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)、さまざまな種類の別のキューに要求を送信するためにフレームワークを指示します。 たとえば、要求が 1 つのキューに配信され、すべての書き込み要求は別のキューに配信をすべて読み取ることを指定できます。

ドライバーが呼び出しや I/O キューのセットを作成するかどうかは[ **WdfDeviceConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff545920)ドライバーは、特定のキューに受け取ることができる要求の種類ごとに、ドライバーは必要はありません、既定のキュー。

ドライバーは、特定の種類の要求を I/O キューを提供しませんし、フレームワークがステータスの完了状態の値をその型の要求を完了すると、ドライバーが関数のドライバーの場合は場合、\_無効な\_デバイス\_要求します。 ドライバーをフィルター ドライバーが呼び出されていて[ **WdfFdoInitSetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff547273)フレームワークは、次の下位ドライバーはドライバー スタックにこれらの要求を自動的に転送します。 そのため、たとえば、フィルター ドライバーは処理されませんの読み取り要求が読み取り要求を受信する I/O キューを提供する必要はありません。

ドライバーが I/O キューを使用する方法の例については、次を参照してください。 [I/O キューの使用例を使用して](example-uses-of-i-o-queues.md)します。

 

 





