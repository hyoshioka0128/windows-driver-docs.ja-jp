---
title: I/O キューのディスパッチ モードの構成
description: I/O キューのディスパッチ モードの構成
ms.assetid: 7603c3fd-a4cb-4174-ad14-f57efedfe9de
keywords:
- WDK UMDF の同期
- キューのディスパッチ モード WDK UMDF
- WDK UMDF モードをディスパッチします。
- WDK UMDF の I/O キュー
- WDK UMDF キュー
- シーケンシャルなディスパッチ モード WDK UMDF
- 並列ディスパッチ モード WDK UMDF
- 手動のディスパッチ モード WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d441a6ad1f7746ec5a3e0efce4a89ef90e88e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536660"
---
# <a name="configuring-dispatch-mode-for-an-io-queue"></a>I/O キューのディスパッチ モードの構成


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

アプリケーションからの I/O 要求が到着したときに、フレームワークは、適切な I/O キューの各要求を配置します。 ドライバーに要求を配信する方法とタイミング、ドライバーが I/O キューのディスパッチを構成する方法、および方法によって異なります、ドライバー[コールバック関数の同期を指定します](specifying-a-callback-synchronization-mode.md)します。 I/O キューが、PnP ともやり取りし、I/O を保持するために UMDF の電源管理サブシステムは、デバイスが適切な状態に到達するまでキューに要求します。

**注**   I/O キューのディスパッチ モードは関連していません、[同期モード](specifying-a-callback-synchronization-mode.md)します。 I/O キューのディスパッチの構成では、表示、要求をキャンセルするイベントのコールバック関数が同時に実行を制御する同期中に、任意の時点で処理するため、ドライバーが受け入れることができる要求の数を制御します。 ただし、操作のいくつかのモードは作成[ディスパッチと同期のモードを組み合わせること](combining-dispatch-and-synchronization-modes.md)します。

 

ドライバーを構成、ドライバーを呼び出すときの I/O キューのディスパッチ、 [ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)メソッドの既定のキューを構成するか、セカンダリ キューを作成します。 ドライバーから値のいずれかを指定できます、 [ **WDF\_IO\_キュー\_ディスパッチ\_型**](https://msdn.microsoft.com/library/windows/hardware/ff552362)で列挙型、 *DispatchType*パラメーターの**IWDFDevice::CreateIoQueue**ディスパッチ モードを識別します。 [I/O キュー オブジェクト](framework-i-o-queue-object.md)次のディスパッチ モードをサポートすることができます。

-   シーケンシャル

    使用してシーケンシャル ディスパッチ モードを指定、 **WdfIoQueueDispatchSequential**値。 このディスパッチ モードでは、キュー処理の状態では、ドライバーでは、一度に 1 つの要求のみが処理されるようにイベントを発生させます。 キューは、ドライバーは、その現在の要求または呼び出しの処理が完了するまでに、追加の要求を遅延、 [ **IWDFIoRequest::ForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff559081)メソッドを要求をキューに再登録します。 現在の要求が完了するか、転送、ときに、キューは、次の要求を提供するイベントを発生させます。

-   Parallel

    使用して並列ディスパッチ モードを指定、 **WdfIoQueueDispatchParallel**値。 このディスパッチ モードでは、キュー処理の状態では、I/O 要求は、ドライバーの準備が整ったとすぐにイベントを発生させます。 ドライバーは、I/O 要求を受け取る、ドライバーは、次の方法のいずれかで、I/O 要求を処理できます。

    -   ドライバーがいずれかを呼び出し、 [ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)または[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)メソッドが完了するにはI/O 要求直後。 ドライバーは、I/O 要求が無効です、これまで処理されることはできません、またはバッファーまたはデータがキャッシュからデータをコピーすることによって行うことができる場合すぐに I/O 要求を完了します。
    -   ドライバーの呼び出し、 [ **IWDFIoRequest::ForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff559081) I/O 要求をキューに再登録するメソッド。
    -   ドライバーの呼び出し、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)下位レベルのドライバーに、I/O 要求を渡す方法です。
-   Manual

    使用して、手動のディスパッチ モードを指定、 **WdfIoQueueDispatchManual**値。 このディスパッチ モードでは I/O キューに自動的に通知が送信されません、ドライバー、キューに着信した要求。 ドライバーを呼び出す必要があります、 [ **IWDFIoQueue::RetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558967)を取得するメソッドは、キューから手動で要求します。 これは、ポーリング モデルです。

    UMDF バージョン 1.9 以降では場合に、ドライバーは、手動のディスパッチ モードを使用して呼び出すことができます[ **IWDFIoRequest2::Requeue** ](https://msdn.microsoft.com/library/windows/hardware/ff559028)のドライバーを取得、I/O キューの先頭に、I/O 要求を返す. 呼び出した後**IWDFIoRequest2::Requeue**、ドライバーの次回の呼び出し[ **IWDFIoQueue::RetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558967)キューに再登録要求を取得します。

すべてのディスパッチ モード、 [I/O キュー オブジェクト](framework-i-o-queue-object.md)を受け取るし、ドライバーが要求を処理するか、要求が取り消されるまで、要求を追跡します。

ドライバーが直列または並列ディスパッチ用のキューを構成した場合、フレームワークは、ドライバーの場合、ドライバー、キューを作成するか、既定のキューを構成します、ドライバーによって登録されているコールバック関数を使用して要求を通知します。 詳細については、[I/O キュー イベントのコールバック関数](i-o-queue-event-callback-functions.md)を参照してください。

 

 





