---
title: I/O キューを管理します。
description: I/O キューを管理します。
ms.assetid: 83cc87c8-7e2d-4f79-a580-0519d327e7ba
keywords:
- WDK KMDF、以降の I/O キュー
- WDK KMDF、停止の I/O キュー
- WDK KMDF、再起動の I/O キュー
- I/O キュー WDK KMDF、要求を追加します。
- I/O キュー WDK KMDF、要求を取得します。
- I/O キュー WDK KMDF、要求の検索
- WDK KMDF、消去の I/O キュー
- WDK KMDF、ドレイン中の I/O キュー
- I/O 要求の移動の WDK KMDF をキューします。
- I/O 要求をインターセプトの WDK KMDF をキューします。
- WDK KMDF、プロパティの I/O キュー
- WDK KMDF を要求する I/O をインターセプト
- 移動の I/O 要求の WDK KMDF
- WDK KMDF を要求する I/O の再配置
- WDK KMDF を要求する I/O の検索
- requeuing I/O 要求の WDK KMDF
- WDK KMDF キューの I/O を停止しています
- WDK KMDF キューの I/O を再起動します。
- WDK KMDF キューの I/O を開始
- WDK KMDF メソッドのディスパッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 970a95d37f56adf13c1f013570535ffe24fea279
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527760"
---
# <a name="managing-io-queues"></a>I/O キューを管理します。


## <a href="" id="starting-an-i-o-queue"></a> I/O キューを開始


ドライバーを呼び出すと[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401) I/O キューを作成するフレームワークが自動的に有効、キューの I/O 要求を受信して、ドライバーに配信します。

ドライバーを呼び出す通常[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)内から、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 フレームワークはドライバーの後に、ドライバーへの I/O 要求の配信を開始できます*EvtDriverDeviceAdd*コールバック関数を返します。

ドライバーが使用されている場合[電源管理対象](using-power-managed-i-o-queues.md)I/O キューの場合は、フレームワーク始めることはできません、ドライバーに要求を提供するまで、デバイスがその稼働状態になるし、フレームワークには、ドライバーが呼び出されて[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)コールバック関数。

## <a href="" id="stopping-and-restarting-an-i-o-queue"></a> 停止して、I/O キューを再起動します。


ドライバーが呼び出せる[ **WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)または[ **WdfIoQueueStopSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548489)からフレームワークを一時的に回避するにはI/O キューからの I/O 要求を配信します。 I/O 要求の配信を再開するドライバーを呼び出す[ **WdfIoQueueStart**](https://msdn.microsoft.com/library/windows/hardware/ff548478)します。

ドライバーは、電源管理対象の I/O キューを使用している場合、フレームワークで、デバイスの作業 (D0) 状態のままし、D0 へのデバイスの状態が返されるときに、フレームワークは、キューを再起動、デバイスのキューが自動的に停止します。

## <a href="" id="adding-requests-to-an-i-o-queue"></a> I/O のキューに要求を追加します。


システムは、ドライバーに読み取り、書き込み、またはデバイスの I/O 操作の要求を送信するときに、フレームワークは、I/O キューに要求を配置します。 ドライバーは、フレームワークは呼び出すことによって、それぞれのキューに格納する要求の種類を制御できます[ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)します。

ドライバーが呼び出すことによって、フレームワークから受信した要求を入れることができますも[ **WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)します。

## <a href="" id="obtaining-requests-from-an-i-o-queue"></a> I/O キューからの要求を取得します。


ドライバーが、順次または並列に指定されている場合[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)、I/O キューの受信要求で[要求ハンドラー](request-handlers.md)します。

ドライバーのマニュアルを指定するか順次メソッドのディスパッチを入手できることの要求を呼び出して[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)または[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)します。

## <a href="" id="searching-for-an-i-o-request"></a> I/O 要求の検索


ドライバーのマニュアルを指定する場合[メソッドのディスパッチ](dispatching-methods-for-i-o-requests.md)が I/O キューの場合は、キュー内の特定の要求を検索する、次の手順を使用します。

1.  呼び出す[ **WdfIoQueueFindRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547415)ドライバーが指定した条件に一致する要求を検索します。

2.  呼び出す[ **WdfIoQueueRetrieveFoundRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548456)要求を取得するを[ **WdfIoQueueFindRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547415)にあります。

## <a href="" id="purging-or-draining-an-i-o-queue"></a> 消去、または、I/O キューのドレイン


*パージ*I/O キューは、キューへの I/O 要求の挿入を停止して、既にキュー内にあるすべての要求をキャンセルすることを意味します。

*ドレイン*I/O キューが既にドライバーに配信される、キュー内にあるすべての要求を許可しているときに、キューへの I/O 要求の挿入の停止を意味します。

ドライバーは、通常消去またはキューが電源の管理されていない場合にのみ、キューのドレインを実行します。 電源管理対象の I/O キューでは、ドライバーを提供できます[ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)と[ *EvtIoResume* ](https://msdn.microsoft.com/library/windows/hardware/ff541779)コールバック関数。

一部のドライバーのキューが電源管理対象でない場合は、消去、またはその関連するデバイスまたは I/O チャネルが使用できなくなった場合、キューのドレインを実行する場合があります。 通常はキューを削除する、ドレインではなくが各要求に非常に重要な情報が含まれている可能性が高くない場合。 たとえば、ネットワーク デバイスのドライバーでは、記憶装置のドライバーは、そのキューをドレイン可能性がありますが、キューがパージ可能性があります。

ドライバーを消去または、I/O キューのドレインを実行する場合は、ドライバーは、次のキュー オブジェクト メソッドのいずれかを呼び出すことができます。

-   [**WdfIoQueuePurge** ](https://msdn.microsoft.com/library/windows/hardware/ff548442)または[ **WdfIoQueuePurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548449)I/O キューの I/O 要求のキューを停止、および未処理の要求を取り消します。

-   [**WdfIoQueueDrain** ](https://msdn.microsoft.com/library/windows/hardware/ff547406)または[ **WdfIoQueueDrainSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff547412)、配信される、既にキューに登録要求を許可しているときに、I/O キューへの I/O 要求のキューを停止して処理されます。

呼び出すときは注意が[ **WdfIoQueueDrain** ](https://msdn.microsoft.com/library/windows/hardware/ff547406)と[ **WdfIoQueueDrainSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff547412)します。 ドレイン操作は、要求の完了の待機、ため、キューの保留中の要求を適切なタイミングで実行することがわかっている場合、キューのみドレインする必要があります。 I/O 要求がどのくらいの期間がわからない場合が完了しては許容未処理の要求をキャンセルし、キューを削除を検討してください。

## <a href="" id="moving-requests-from-one-i-o-queue-to-another"></a> 1 つの I/O キューからの要求の移動


ドライバーが、I/O 要求を受け取った後は、別の I/O キューに要求をもう一度キューにドライバーをする可能性があります。 これには、ドライバーの呼び出しを行う[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)または[ **WdfRequestForwardToParentDeviceIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549959)、追加、指定したキューの末尾を要求します。 最終的には、フレームワークは配信要求のドライバーにもう一度指定したキューのディスパッチ メソッドを使用しています。 1 つの I/O キューから別の I/O 要求の移動の詳細については、[I/O 要求の Requeuing](requeuing-i-o-requests.md)を参照してください。

## <a href="" id="intercepting-an-i-o-request-before-it-is-queued"></a> キューに配置する前に、I/O 要求をインターセプト


ドライバー、フレームワークは、I/O キューに要求を配置する前に、I/O 要求をインターセプトすることができます。 I/O 要求をインターセプトするドライバーを呼び出す必要があります[ **WdfDeviceInitSetIoInCallerContextCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546119)を登録する、 [ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)コールバック関数。

フレームワークを関連付けます、 [ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)デバイスとコールバック関数。 その結果、フレームワーク、 *EvtIoInCallerContext*システムは、デバイスに送信する要求を受信するたびに、コールバック関数。

通常、ときに、 [ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)コールバック関数は要求を受け取る、要求のいくつかの事前処理を実行します。 次に、コールバック関数を呼び出す[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945)フレームワークに、要求は戻る、します。 フレームワークはが呼び出さない場合と同様、適切な I/O キューの要求を配置できます、 *EvtIoInCallerContext*コールバック関数。

ドライバーが提供する主な理由、 [ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)と呼ばれる I/O メソッドをサポートする I/O 操作を処理するために、ドライバーがあるコールバック関数は、[もないです。バッファー内や直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff540701#neither)します。 この I/O メソッドでは、ドライバーは、I/O 要求の発信元のプロセスのコンテキストで受信したバッファーにアクセスする必要があります。 詳細については、[Framework ベースのドライバーでのデータ バッファーへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff540701)を参照してください。

## <a href="" id="obtaining-i-o-queue-properties"></a> I/O キューのプロパティを取得します。


フレームワークのキュー オブジェクトのプロパティを取得するには、ドライバーは、次のメソッドを呼び出すことができます。

-   [**WdfIoQueueGetDevice**](https://msdn.microsoft.com/library/windows/hardware/ff547421)、キュー オブジェクトが属するデバイス オブジェクトを識別するハンドルを取得します。

-   [**WdfIoQueueGetState**](https://msdn.microsoft.com/library/windows/hardware/ff548437)を取得するには、[状態情報](i-o-queue-states.md)キューに関するします。

 

 





