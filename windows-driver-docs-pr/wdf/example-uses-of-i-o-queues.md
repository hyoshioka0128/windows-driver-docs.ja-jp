---
title: I/O キューの使用例
description: I/O キューの使用例
ms.assetid: 13b09254-ce0a-4c7d-bdb1-d28ec094a266
keywords:
- WDK KMDF、例の I/O キュー
- 要求ハンドラー WDK KMDF
- 既定の I/O キュー WDK KMDF
- 1 つの I/O キュー WDK KMDF
- 複数の I/O キュー WDK KMDF
- 並列 I/O キュー WDK KMDF
- シーケンシャル I/O キュー WDK KMDF
- 手動の I/O キュー WDK KMDF
- I/O キュー WDK KMDF、メソッドのディスパッチ
- WDK KMDF メソッドのディスパッチ
- シーケンシャルなディスパッチ WDK KMDF
- 同期のディスパッチ WDK KMDF
- 並列のディスパッチ WDK KMDF
- 非同期ディスパッチ WDK KMDF
- 手動のディスパッチ WDK KMDF
- WdfIoQueueDispatchParallel
- WdfIoQueueDispatchSequential
- WdfIoQueueDispatchManual
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3539c02c7fd9a2f20d43049ba8f9a7f5a5238b2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539068"
---
# <a name="example-uses-of-io-queues"></a>I/O キューの使用例





システムに接続され、特定のドライバーがサポートされている各デバイスのドライバーが次の I/O キューの組み合わせを使用でき、[要求ハンドラー](request-handlers.md):

-   1 つ、既定の I/O キューおよび、1 つの要求ハンドラー [ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)します。 フレームワークは、既定のキューにすべてのデバイスの要求を配信し、ドライバーを呼び出すことが、 *EvtIoDefault*ドライバーに各要求を配信するハンドラー。

-   1 つ、既定の I/O キューと複数のハンドラーが要求など[ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)、 [ *EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)、および[ *EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)します。 フレームワークは、既定のキューにすべてのデバイスの要求では提供します。 ドライバーを呼び出すことが、 *EvtIoRead*読み取りの要求を配信するハンドラー、 *EvtIoWrite*書き込み要求を配信するハンドラーと*EvtIoDeviceControl*ハンドラーデバイス I/O 制御要求を提供します。

-   読み取り要求の 1 つのもう 1 つの書き込み要求などの複数 I/O キュー。 キューごとには、ドライバーは、キューが要求の種類を 1 つだけを受信するために 1 つだけ要求ハンドラーを提供します。

-   複数の I/O キュー、それぞれに複数の要求ハンドラー。

一部のシナリオの例は次のとおりです。

-   [1 つのシーケンシャル I/O キュー](#a-single-sequential-io-queue)

-   [複数のシーケンシャル I/O キューと手動のキュー](#multiple-sequential-io-queues-and-a-manual-queue)

-   [1 つの並列 I/O キュー](#a-single-parallel-io-queue)

-   [複数の並列 I/O キュー](#multiple-parallel-io-queues)

## <a name="a-single-sequential-io-queue"></a>1 つのシーケンシャル I/O キュー

できる唯一のサービス読み取りおよび書き込み要求 1 つずつ関数ドライバー ディスク ドライブを作成する場合、関数ドライバーには、デバイスごとに 1 つだけの I/O キューが必要があります。

ドライバーはドライバーを呼び出すときにフレームワークによって作成される既定の I/O キューを使用できます[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)設定と**DefaultQueue**に**TRUE**でキューの[ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)構造体。 WDF\_IO\_キュー\_構成構造体のドライバーを指定する必要がありますも。

-   **WdfIoQueueDispatchSequential**ディスパッチのメソッドとしてそのため、既定の I/O キューが I/O 要求を配信ドライバー同期的にします。

-   1 つのイベントのコールバック関数では、 [ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)、すべての I/O 要求を受信します。

たびに、I/O 要求は、ドライバーの既定の I/O キューで利用できるフレームワークが要求を配信、ドライバーを呼び出してドライバーの[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)要求ハンドラー。 別の要求が、キューで使用可能になると、フレームワークは配信しませんが、ドライバーの呼び出しまで[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)の前に配信された要求。

## <a name="multiple-sequential-io-queues-and-a-manual-queue"></a>複数のシーケンシャル I/O キューと手動のキュー

次の特性を持つシリアル ポートのデバイスを検討してください。

-   1 つを同時に実行できる操作と書き込み操作の読み取り。

-   実行の複数の読み取りまたは書き込み操作を非同期的にできません。

-   状態の情報をデバイスの I/O 制御要求を受信できます。 デバイスのドライバーでは、これらの要求 (要求の状態の変更を待機する場合) などの一部を完了に時間をかかる場合があります。

関数のドライバー シーケンシャル I/O キュー デバイスごとにこのデバイスは、複数を使用できます、します。 ドライバーを呼び出して[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401) 3 回: 既定のキューを作成して、その他の 2 つの I/O キューを作成するには、2 回に 1 回です。 [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359) 、これらのキューの各構造体をドライバーを指定する必要があります。

-   **WdfIoQueueDispatchSequential**キューごとに、ディスパッチ方法として、フレームワークは、ドライバーを I/O 要求を同期的に配信ができるようにします。

-   異なる[要求ハンドラー](request-handlers.md)キューごとに ([*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)、 [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)、および[*EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813))、キューの I/O 要求を受け取ります。

呼び出した後[ **WdfIoQueueCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547401)、ドライバーを呼び出すことが[ **WdfDeviceConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff545920)前方のすべてを 2 回 -その他のキューのいずれかに対する読み取り要求と、他のすべての書き込み要求。

この構成では、デバイスの既定の I/O キュー [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)状態の情報をデバイス I/O 制御要求にコールバック関数が表示されます。

状態要求を長時間保持するために、ドライバーがある場合、4 番目のキューを作成し、指定**WdfIoQueueDispatchManual**ディスパッチ メソッドとして。 ドライバーが待つ必要がある情報の要求を受け取ったときに、この余分なキューに要求を配置して、状態情報が使用可能になるまでにできます。 ドライバーは、要求をキューから取得、完了します。 それまでは、既定のキューでは、ドライバーを別の要求を配信できます。

## <a name="a-single-parallel-io-queue"></a>1 つの並列 I/O キュー

IDE ディスク コント ローラーは、一部の I/O 操作が、オーバー ラップできます。 たとえば、コント ローラーが 1 つのディスクの読み取りまたは書き込み操作を処理中には、別のディスクにシーク コマンドを送信できます。 その一方で、複数の同時読み取りし、書き込みコマンドはサポートされていません。

このコント ローラーの機能のドライバーは、I/O 要求ごとに調べる必要があります。 ドライバーは、シーク コマンドを受信する場合、シーク コマンドを処理できるかどうかはそれを判断する必要があります。 場合、シーク コマンドを処理できません。

-   指定したディスク ドライブがビジー状態では既にです。

-   ディスク ドライブは書式設定されると、そのため、他のドライブ アクティブにできるありません。

コント ローラーに接続されている各デバイス ドライバーを呼び出すことが[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)を既定の I/O キューを作成します。 [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359) 、これらのキューの各構造体をドライバーを指定する必要があります。

-   **WdfIoQueueDispatchParallel**キューごとに、ディスパッチ方法として、フレームワークは、ドライバーを I/O 要求を非同期的に配信ができるようにします。

-   [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)キューごとに、キューの I/O 要求を受信するイベントのコールバック関数。

この構成では、1 つの並列 I/O キューは、各デバイスに割り当てられます。 ドライバーは、フレームワークは、各 I/O キューから配信する I/O 要求ごとに調べる必要があります。 ドライバーは要求をすぐに処理できる場合は。 それ以外の場合、ドライバーを呼び出す[ **WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)、ドライバーの呼び出しまでの要求の配信を停止するためにフレームワークが[ **WdfIoQueueStart**](https://msdn.microsoft.com/library/windows/hardware/ff548478).

## <a name="multiple-parallel-io-queues"></a>複数の並列 I/O キュー

SCSI ホスト アダプターでは、非同期オーバー ラップ I/O 操作をサポートするデバイスの例を示します。 アダプターには、最大 32 のデバイスを接続できます。 次の構成でのシステムを考慮してください。

-   SCSI アダプターのサポート「済」に接続されている一部のデバイスとないものです。 SCSI デバイス済をサポートする場合、I/O 操作中にデバイス一時的に解放できますアダプターのため、アダプターが別のデバイスをサービスします。 後で、最初のデバイスでは、自体の操作を完了再選択します。

-   SCSI アダプターでは、ハードウェアのメールボックスを使用して、ドライバーとデバイスの間の要求と応答を渡します。 デバイスが要求の準備が使用可能なメールボックスがない場合、デバイスが待つ必要があります。

最適なパフォーマンスをこの SCSI ホスト アダプターの機能のドライバーは使用するとすぐに、フレームワークから I/O 要求を受信する必要があります。 ドライバーは、各要求を確認しますし、利用できるリソース (メールボックス メモリなど)、およびデバイスまで延期する必要があります、またはすぐに開始できますを判別する必要があります。

ドライバーは、複数を使用して、I/O キューを並列する必要があります可能性があります。 アダプターに接続されている各デバイス ドライバーを呼び出すと[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)を既定の I/O キューを作成します。 [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359) 、これらのキューの各構造体をドライバーを指定する必要があります。

-   **WdfIoQueueDispatchParallel**キューごとに、ディスパッチ方法として、フレームワークは、ドライバーを I/O 要求を非同期的に配信ができるようにします。

-   [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)キューごとに、キューの I/O 要求を受信するイベントのコールバック関数。

各 I/O キューの[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)が配信され、すぐに 1 つずつ処理されるかどうかを判断、コールバック関数は、キューの I/O 要求を調べる必要があります。 デバイスとシステム リソースが使用可能な場合は、ドライバーは、I/O 操作を開始します。 デバイスまたはリソースが利用できない場合、ドライバーを呼び出す必要があります[ **WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)まで、現在の 1 つを処理できる追加の要求の配信が停止します。

ドライバーを呼び出すことができます必要に応じて、 [ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)デバイスごとにその他のキューを作成します。 ドライバーを呼び出すことができますし、 [ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)をいくつかの種類の他のキューに要求をキューに再登録します。 フレームワークは、その他のキューからの要求を配信するときに、ドライバーを呼び出すことができます[ **WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)必要に応じて、そのキュー数または種類の最小限に抑えるため、既定のキューではなく、要求は配信が延期されます。

 

 





