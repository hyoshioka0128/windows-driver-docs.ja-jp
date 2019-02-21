---
title: I/O 要求のディスパッチ メソッド
description: I/O 要求のディスパッチ メソッド
ms.assetid: 3e91aa7c-bccf-4eeb-8b68-b1277a690f8c
keywords:
- I/O キューの作成の WDK KMDF
- I/O キュー WDK KMDF、メソッドのディスパッチ
- WDK KMDF メソッドのディスパッチ
- シーケンシャルなディスパッチ WDK KMDF
- 同期のディスパッチ WDK KMDF
- 並列のディスパッチ WDK KMDF
- 非同期ディスパッチ WDK KMDF
- 手動のディスパッチ WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191ff93f32acfb5e757da2253a678c8cdff1cfe9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536558"
---
# <a name="dispatching-methods-for-io-requests"></a>I/O 要求のディスパッチ メソッド





ドライバーを呼び出すと[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401) I/O キューを作成するキューのディスパッチ メソッドを指定します。 フレームワークは、次の 3 つのディスパッチ メソッドを提供します:[シーケンシャル](#sequential-dispatching)、[並列](#parallel-dispatching)、および[手動](#manual-dispatching)します。 ドライバーを指定できますいずれデバイスを含む、すべての I/O キューのメソッドのディスパッチ[既定の I/O キュー](creating-i-o-queues.md)します。

ドライバーでは、キューのディスパッチ メソッドを設定を指定して、 [ **WDF\_IO\_キュー\_ディスパッチ\_型**](https://msdn.microsoft.com/library/windows/hardware/ff552362)-キューのに型指定された値[**WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)構造体。

たとえば、各ディスパッチ メソッドの使用方法を参照してください[I/O キューの使用例を使用して](example-uses-of-i-o-queues.md)します。

### <a href="" id="sequential-dispatching"></a> シーケンシャルなディスパッチ

使用するデバイスの I/O キューを設定する必要がある場合は、ドライバーまたはデバイスでは、キューから 1 つだけの I/O 要求を一度に処理できる、*シーケンシャル ディスパッチ*と呼ばれるも*同期ディスパッチ*します。 フレームワークは、この種類のディスパッチのでは、要求を一度に 1 つ、ドライバーに配信します。 フレームワークでは、ドライバーまで、次の要求を配信しません[完了](completing-i-o-requests.md)、[キャンセル](canceling-i-o-requests.md)、または[requeues](requeuing-i-o-requests.md)前回の要求。

フレームワークのドライバーのいずれかに要求の配信後[要求ハンドラー](request-handlers.md)、ドライバー[要求を処理します](processing-i-o-requests.md)します。 ドライバーが要求を転送する場合、[一般的な I/O ターゲット](general-i-o-targets.md)、I/O ターゲット オブジェクトの同期メソッドのいずれかを通常に呼び出します。 これらのメソッドの詳細については、次を参照してください。[同期に I/O 要求を送信する](sending-i-o-requests-synchronously.md)します。 ドライバーに最終的にする必要があります[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)I/O キューから受信したすべての要求。

シーケンシャルなディスパッチを呼び出すことができますが、I/O キューがセットアップされているドライバー [ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)または[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)最後の前に、キューから別の要求を取得する受信した要求が完了またはキャンセルされました。 ドライバーがドライバーの中に次のハードウェアの操作を開始できるように関数ドライバーでこれを行う場合[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数には、前のデータがまだ処理ハードウェアの操作です。

いくつかの I/O キューを作成し、シーケンシャル ディスパッチすべてでは設定すると、フレームワークが順番に各キューからの要求をディスパッチがキューを並列で実行します。 ドライバーまたはデバイスは、任意の型は、一度に 1 つの要求を処理できる場合に、1 つの I/O キューを使用する必要があります、 [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)コールバック関数。

### <a href="" id="parallel-dispatching"></a> 並列のディスパッチ

使用するデバイスの I/O キューを設定することができる場合、ドライバーとデバイス I/O 要求を複数同時に処理できる、*並列ディスパッチ*ドライバーでは、要求を非同期的に処理できるようにします。 このディスパッチのメソッドが呼び出されますも*非同期ディスパッチ*します。

ドライバーで、I/O キューを設定すると、並列のディスパッチを使用して場合、フレームワークは、キューでは使用するとすぐに、ドライバーを I/O 要求を配信します。 結果は、ドライバーは、一度に複数の要求を処理する必要があります。

たびに、ドライバーのいずれかの[要求ハンドラー](request-handlers.md)要求を受信、ドライバーである必要があります[要求を処理](processing-i-o-requests.md)し[完了](completing-i-o-requests.md)要求。 ドライバーが要求を転送する場合、[一般的な I/O ターゲット](general-i-o-targets.md)、I/O ターゲット オブジェクトの非同期メソッドのいずれかを通常に呼び出します。 これらのメソッドの詳細については、次を参照してください。 [I/O の要求を非同期に送信する](sending-i-o-requests-asynchronously.md)します。 ドライバーに最終的にする必要があります[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)I/O キューから受信したすべての要求。

並列のディスパッチを使用するドライバーを呼び出すことができます[ **WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)または[ **WdfIoQueueStopSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548489)を一時的に停止します。キュー、および呼び出して[ **WdfIoQueueStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548478)キューを再起動します。

### <a href="" id="manual-dispatching"></a> 手動のディスパッチ

使用するデバイスの I/O キューを設定することができます、ドライバーが I/O 要求の配信を完全に制御する場合は、*手動ディスパッチ*、つまり、あるフレームワークが含まれていません要求ドライバーにしない限り、ドライバーいずれかが明示的に要求します。

手動のキューからの要求を取得するドライバーを呼び出すことができます[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)または[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)キューをポーリングするループ内で。 ドライバーを呼び出すことができますも[ **WdfIoQueueReadyNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff548452)を 1 つまたは複数の要求が、キューで利用できるときにフレームワークが呼び出すコールバック関数を登録します。 フレームワークは、コールバック関数を呼び出し、ドライバーを呼び出すことが**WdfIoQueueRetrieveNextRequest**または**WdfIoQueueRetrieveRequestByFileObject**ループ、要求を取得します。

ドライバーは、キューから要求を取得した後にする必要があります[要求を処理](processing-i-o-requests.md)します。 ドライバーに最終的にする必要があります[完了](completing-i-o-requests.md)または[キャンセル](canceling-i-o-requests.md)各要求。

 

 





