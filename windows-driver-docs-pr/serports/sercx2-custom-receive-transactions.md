---
title: SerCx2 カスタム受信トランザクション
description: シリアル コント ローラーの一部のハードウェア シリアル コント ローラーからデータを読み取る PIO またはシステム DMA 以外のデータ転送メカニズムを実装できます。
ms.assetid: 29849A8C-6656-444C-BE91-405A4BA2D5B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1f59361bf58c86feda6017300b8a0aed023ce5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539351"
---
# <a name="sercx2-custom-receive-transactions"></a>SerCx2 カスタム受信トランザクション


シリアル コント ローラーの一部のハードウェア シリアル コント ローラーからデータを読み取る PIO またはシステム DMA 以外のデータ転送メカニズムを実装できます。 シリアル コント ローラー ドライバーがサポートできるカスタム受信トランザクションがこのデータ転送メカニズム SerCx2 で使用できるようにします。

開始する、カスタムのトランザクションの受信、SerCx2 呼び出しのドライバーの[ *EvtSerCx2CustomReceiveTransactionStart* ](https://msdn.microsoft.com/library/windows/hardware/dn265204)イベント コールバック関数、読み取りをパラメーターとして提供し、([ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) 要求とトランザクションの読み取りバッファーの説明。 この呼び出しでは、関数は、トランザクションを開始し、返します。 ドライバーは、トランザクションを完了して、読み取り要求を完了する責任を負います。

## <a name="creating-the-custom-receive-object"></a>Custom-receive オブジェクトを作成します。


SerCx2 がコント ローラーのシリアル ドライバーを呼び出す前に*EvtSerCx2CustomReceiveTransaction*Xxx * * 関数の場合、ドライバーが呼び出す必要があります、 [ **SerCx2CustomReceiveTransactionCreate**](https://msdn.microsoft.com/library/windows/hardware/dn265251) SerCx2 をこれらの関数を登録するメソッド。 このメソッドは、入力パラメーターとしてへのポインターを[ **SERCX2\_カスタム\_受信\_トランザクション\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn265315)構造体ドライバーへのポインターを含む*EvtSerCx2CustomReceiveTransaction*Xxx * * 関数。

ドライバーは、次の 2 つの関数を実装する必要があります。

-   [*EvtSerCx2CustomReceiveTransactionStart*](https://msdn.microsoft.com/library/windows/hardware/dn265204)
-   [*EvtSerCx2CustomReceiveTransactionQueryProgress*](https://msdn.microsoft.com/library/windows/hardware/dn265203)

オプションとして、ドライバーは、次の 3 つの関数の一部またはすべてを実装できます。

-   [*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*](https://msdn.microsoft.com/library/windows/hardware/dn265201)
-   [*EvtSerCx2CustomReceiveTransactionInitialize*](https://msdn.microsoft.com/library/windows/hardware/dn265202)
-   [*EvtSerCx2CustomReceiveTransactionCleanup*](https://msdn.microsoft.com/library/windows/hardware/dn265200)

**SerCx2CustomReceiveTransactionCreate**メソッド custom-receive オブジェクトを作成し、呼び出し元のドライバーを提供する[ **SERCX2CUSTOMRECEIVETRANSACTION** ](https://msdn.microsoft.com/library/windows/hardware/dn265249)このオブジェクトへのハンドルします。 ドライバーの*EvtSerCx2CustomReceiveTransaction*Xxx * * すべての関数は、最初のパラメーターとしてこのハンドルを受け取ります。 次の SerCx2 メソッドは、最初のパラメーターとして、このハンドルを受け取ります。

-   [**SerCx2CustomReceiveTransactionNewDataNotification**](https://msdn.microsoft.com/library/windows/hardware/dn265253)
-   [**SerCx2CustomReceiveTransactionReportProgress**](https://msdn.microsoft.com/library/windows/hardware/dn265254)
-   [**SerCx2CustomReceiveTransactionInitializeComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265252)
-   [**SerCx2CustomReceiveTransactionCleanupComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265250)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ


シリアル コント ローラーのドライバーによっては、シリアル コント ローラーのハードウェアの開始時に初期化する必要があります、カスタム受信トランザクション、またはトランザクションの最後に、シリアル コント ローラーのハードウェアの状態をクリーンアップします。

ドライバーが実装されている場合、 [ *EvtSerCx2CustomReceiveTransactionInitialize* ](https://msdn.microsoft.com/library/windows/hardware/dn265202)イベント コールバック関数では、SerCx2 がトランザクションを開始する前に、シリアル コント ローラーを初期化するには、この関数を呼び出します。 実装されている場合、 *EvtSerCx2CustomReceiveTransactionInitialize*関数を呼び出す必要があります、 [ **SerCx2CustomReceiveTransactionInitializeComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265252)メソッドドライバーでは、シリアル コント ローラーの初期化が完了すると、SerCx2 を通知します。

ドライバーが実装されている場合、 [ *EvtSerCx2CustomReceiveTransactionCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn265200)イベント コールバック関数、SerCx2 がトランザクションの終了後に、ハードウェアの状態をクリーンアップするには、この関数を呼び出します。 実装されている場合、 *EvtSerCx2CustomReceiveTransactionInitialize*関数を呼び出す必要があります、 [ **SerCx2CustomReceiveTransactionCleanupComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265250)に通知するメソッドSerCx2 ドライバーでは、シリアル コント ローラーのクリーンアップが完了するとします。

## <a name="new-data-notifications"></a>新しいデータの通知


オプションとして、シリアル コント ローラー ドライバーを実装できる、 [ *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification* ](https://msdn.microsoft.com/library/windows/hardware/dn265201)イベント コールバック関数。 実装されている場合、SerCx2 はこの関数を使用して、カスタムの受信トランザクションとして処理される読み取り要求の処理中に発生する間隔のタイムアウトを効率的に管理します。

間隔、タイムアウトは、シリアル コント ローラーで受信した 2 つの連続するバイトまでの間隔は、クライアントが指定した最大時間を超えた場合に発生します。 SerCx2 に周辺機器のドライバーが読み取り要求を送信すると後に、少なくとも 1 バイトのデータを逐次的に接続されている周辺機器のデバイスから受信した後までの間隔、タイムアウトは発生しません。 到着までの時間は、読み取り要求と周辺機器のデバイスからのデータの最初のバイトの受信、最初のバイトを受信した後、残りの読み取り要求のデータを受信するために必要な時間よりも大幅に長くする場合可能性があります。 詳細については、[**シリアル\_タイムアウト**](https://msdn.microsoft.com/library/windows/hardware/hh439614)を参照してください。

SerCx2 呼び出し、 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*関数を実装すると、新しいデータ通知を有効にする場合。 この通知が有効になりシリアル コント ローラーは、周辺機器のデバイスから新しいデータの 1 つまたは複数のバイトを受信したり、既にデータがある場合、FIFO の受信、シリアル コント ローラーのドライバーを呼び出す必要があります、 [ **SerCx2CustomReceiveTransactionNewDataNotification** ](https://msdn.microsoft.com/library/windows/hardware/dn265253) SerCx2 に通知するメソッド。

SerCx2 可能な間隔のタイムアウトを検出するために呼び出す定期的に、 [ *EvtSerCx2CustomReceiveTransactionQueryProgress* ](https://msdn.microsoft.com/library/windows/hardware/dn265203)中にすべてのデータが受信したかどうかをチェックするイベントのコールバック関数、前の間隔。 シリアル コント ローラー ドライバーが実装するかどうかによって異なります SerCx2 によるデータの最初のバイトの受信の検出、 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*関数。 この関数が実装されている場合、SerCx2 は、新しいデータ通知を有効にする関数を呼び出すし、データの最初のバイトが受信したときに、ドライバーによって通知されます。 SerCx2 が定期的に呼び出して、それ以外の場合、 *EvtSerCx2CustomReceiveTransactionQueryProgress*関数の最初のバイトの受信を検出して、これらの呼び出しを実行するプロセッサを定期的にスリープ解除する必要があります。 したがって、実装するドライバー、 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*関数は、プロセッサを何度でもスリープ解除する必要がない電力消費量を減らすことができます。

SerCx2 は、保留中の新しいデータに関する通知を明示的に取り消されません、トランザクションをカスタム受信します。 ただし、シリアル コント ローラー ドライバーが、通知を有効にし、次の理由の 1 つのドライバーが関連付けられている読み取り要求を完了する必要があります暗黙的に新しいデータ通知をキャンセルする必要があります。

-   読み取り要求がタイムアウトになるかが取り消されます。
-   シリアル コント ローラーでは、低電力状態に入ろう D0 デバイスの電源状態を終了しようとしています。

ドライバーでメソッドをなど、呼び出す通常[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)要求を完了します。 ドライバーは呼び出す必要がありますしない**SerCx2CustomReceiveTransactionNewDataNotification**要求が完了した後。

## <a name="accessing-the-request-object"></a>要求オブジェクトへのアクセス


開始する、カスタムのトランザクションの受信、SerCx2 呼び出しのドライバーの[ *EvtSerCx2CustomReceiveTransactionStart* ](https://msdn.microsoft.com/library/windows/hardware/dn265204)関数と関連付けられている読み取り (WDFREQUEST オブジェクトでカプセル化された要求パスハンドル) この関数をパラメーターとして。 ドライバーは、メソッドの呼び出しを担当[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)トランザクションが完了すると、この要求を完了します。 要求を完了しない限り、すぐに、前に、 *EvtSerCx2CustomReceiveTransactionStart*関数を返します、ドライバーはなどのメソッドを呼び出す必要があります[ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)要求をキャンセル可能としてマークします。

シリアル コント ローラー ドライバーがなど、メソッドを使用しない必要があります[ **WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018)読み取り要求のデータ バッファーにアクセスします。 代わりに、ドライバーを使用する必要があります、 *Mdl*、*オフセット*、および*長さ*に渡されるパラメーター値、 *EvtSerCx2CustomReceiveTransactionStart*このバッファーにアクセスする関数。

中に、カスタムのトランザクションの受信、ドライバーは、要求オブジェクトに関連付けられているコンテキストに、トランザクションに関する情報を格納する必要があります。 そうである場合、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)イベント コールバック関数を呼び出すことができます、 [ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)メソッド要求オブジェクトに使用する属性を設定します。 これらの属性には、要求コンテキストを使用する名前と割り当てのサイズが含まれます。 この呼び出しで指定された要求属性は、ドライバーをへの呼び出しで指定する要求属性に一致する必要があります、 [ **SerCx2InitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/dn265261)メソッド。 これらの属性がで指定された、 **RequestAttributes**のメンバー、 **SERCX2\_CONFIG**ドライバーに渡します構造**SerCx2InitializeDevice**. 詳細については、[ **SERCX2\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn265310)を参照してください。

開始時シリアル コント ローラー ドライバーが受信した読み取り要求をカスタムのトランザクションの受信、ドライバー、フレームワークによって割り当てられている要求コンテキストが初期化されていません。 ドライバー呼び出す必要があります、ベスト プラクティスとして、 [ **RtlZeroMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563610)ルーチンをすべてゼロには、この要求コンテキストを初期化します。

 

 




