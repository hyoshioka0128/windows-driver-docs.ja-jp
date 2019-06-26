---
Description: USB デバイスは、送信または一定の間隔でデータを受信できるように、割り込みのエンドポイントをサポートできます。
title: USB 割り込み転送要求の送信方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d294b7beb2e1be0ba8566faea72261b771a631
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378291"
---
# <a name="how-to-send-a-usb-interrupt-transfer-request-uwp-app"></a>USB 割り込み転送要求の送信方法 (UWP アプリ)


**要約**

-   割り込みホストがデバイスをポーリングするときに、転送が発生します。
-   イベント ハンドラーを実装[ **UsbInterruptInPipe.DataReceived**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)
-   登録およびイベント ハンドラーを登録解除

**重要な API**

-   [**UsbInterruptInPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)
-   [**UsbInterruptOutPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)
-   [**UsbInterruptInEventArgs**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEventArgs)

USB デバイスは、送信または一定の間隔でデータを受信できるように、割り込みのエンドポイントをサポートできます。 これを実現する、ホストは一定の間隔でデバイスをポーリングし、データが転送されるたびに、ホストがデバイスをポーリングします。 割り込み転送は、デバイスからの割り込みのデータを取得するためほとんど使用されます。 このトピックでは、UWP アプリがデバイスから継続的な割り込みデータを取得する方法について説明します。

**エンドポイント情報を中断します。**

割り込みのエンドポイントについては、記述子は、これらのプロパティを公開します。 これらの値が参照するだけ、バッファー転送を管理する方法に影響はありません。

-   データの送信頻度を指定できますか。

    取得することでその情報を取得、**間隔**エンドポイント記述子の値 (を参照してください[ **UsbInterruptOutEndpointDescriptor.Interval** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Interval)または[ **UsbInterruptInEndpointDescriptor.Interval**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor#Windows_Devices_Usb_UsbInterruptInEndpointDescriptor_Interval))。 値がどのくらいの頻度を示すデータが送信またはバス上の各フレーム内のデバイスから受信します。

    **注**、**間隔**プロパティは、 **bInterval** (USB 仕様で定義された) 値。

    値がどのくらいの頻度を示すことに、またはデバイスからデータを転送します。 たとえば、高速デバイス場合**間隔**125 (マイクロ秒) は、データが転送されるすべての 125 (マイクロ秒)。 場合**間隔**1000 (マイクロ秒) では、データが転送されるミリ秒単位。

-   データの量は、各サービスの間隔で転送できますか。

    エンドポイント記述子でサポートされている最大パケット サイズを取得することで送信できるバイト数を取得する (UsbInterruptOutEndpointDescriptor.MaxPacketSize または UsbInterruptInEndpointDescriptor.MaxPacketSize を参照してください。 パケットの最大サイズは、デバイスの速度で制限。 最大 8 バイトの低速デバイス。 最大 64 バイトのフル スピード デバイス。 高速で高帯域幅のデバイスのアプリを送信または受信パケットの最大サイズは microframe あたり最大 3072 バイト以上。

    **注**SuperSpeed デバイスでの割り込みのエンドポイントがさらに多くのバイト数を送信することです。 値がで示される、 **wBytesPerInterval** USB の\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子。 記述子を取得するを使用して、記述子のバッファーを取得、 [ **UsbEndpointDescriptor.AsByte** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_AsByte)プロパティとを使用してバッファーに格納し解析[ **DataReader**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader)メソッド。



**転送を中断**

USB デバイスは、一定の間隔で、ホストからデータを受信する割り込みアウト エンドポイントをサポートできます。 ホストが、デバイスをポーリングするたびに、ホストは、データを送信します。 UWP アプリでは、転送要求を送信するデータを指定する、割り込みを開始できます。 デバイスには、ホストからのデータが確認されるときに、その要求が完了しました。 UWP アプリはデータを書き込むことができます、 [ **UsbInterruptOutPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)します。

**中断中の転送**

逆に、USB デバイス、デバイスによって生成されたハードウェアの割り込みについて、ホストに通知する手段として、割り込みのエンドポイントをサポートできます。 通常 USB ヒューマン インターフェイス デバイス (HID) キーボードなどとのポインティング デバイスは、エンドポイントの割り込みをサポートします。 割り込みが発生するときに、エンドポイントは、データが、ホストをすぐに到達できませんが、割り込みのデータを格納します。 エンドポイントは、デバイスをポーリングするホスト コント ローラーを待つ必要があります。 最低限がある必要がありますので、時刻のデータ間の遅延が生成され、ホストに到達、一定の間隔でデバイスをポーリングします。 UWP アプリで受信したデータを取得できます、 [ **UsbInterruptInPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)します。 ホストによって、デバイスからのデータを受信したときに完了した要求。

## <a name="before-you-start"></a>はじめに...


-   デバイスを開いて、取得する必要がありますが、 [ **UsbDevice** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)オブジェクト。 読み取り[USB デバイス (UWP アプリ) に接続する方法](how-to-connect-to-a-usb-device--uwp-app-.md)します。
-   Scenario3 CustomUsbDeviceAccess サンプルでは、このトピックに示す完全なコードを確認できます\_InterruptPipes ファイル。

## <a name="writing-to-the-interrupt-out-endpoint"></a>外部エンドポイント割り込みへの書き込み


転送要求を割り込みに一括転送のターゲットを除く、アウトと同じですが、アプリに送信する方法は、割り込みによって表される、パイプを[ **UsbInterruptOutPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)します。 詳細については、次を参照してください。 [USB 一括転送要求 (UWP アプリ) を送信する方法](how-to-send-a-usb-bulk-transfer--uwp-app-.md)します。

## <a name="step-1-implement-the-interrupt-event-handler-interrupt-in"></a>手順 1:(割り込みの) 割り込みイベント ハンドラーを実装します。


割り込みパイプにデータがデバイスから受信されると、生成、 [ **DataReceived** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)イベント。 割り込みのデータを取得するには、アプリは、イベント ハンドラーを実装する必要があります。 *EventArgs*ハンドラーのパラメーターは、データ バッファーを指します。

このコードの例では、イベント ハンドラーの単純な実装を示します。 ハンドラーは、割り込みの受信のカウントを保持します。 ハンドラーが呼び出されるたびにカウントをインクリメントします。 ハンドラーからのデータ バッファーを取得する*eventArgs*パラメーターと受信の割り込みの数とバイトの長さが表示されます。

```CSharp
private async void OnInterruptDataReceivedEvent(UsbInterruptInPipe sender, UsbInterruptInEventArgs eventArgs)
{
    numInterruptsReceived++;

    // The data from the interrupt
    IBuffer buffer = eventArgs.InterruptData;

    // Create a DispatchedHandler for the because we are interracting with the UI directly and the
    // thread that this function is running on may not be the UI thread; if a non-UI thread modifies
    // the UI, an exception is thrown

    await Dispatcher.RunAsync(
                       CoreDispatcherPriority.Normal,
                       new DispatchedHandler(() =>
    {
        ShowData(
        "Number of interrupt events received: " + numInterruptsReceived.ToString()
        + "\nReceived " + buffer.Length.ToString() + " bytes");
    }));
}
```

```ManagedCPlusPlus
void OnInterruptDataReceivedEvent(UsbInterruptInPipe^ /* sender */, UsbInterruptInEventArgs^  eventArgs )
{
    numInterruptsReceived++;

    // The data from the interrupt
    IBuffer^ buffer = eventArgs->InterruptData;

    // Create a DispatchedHandler for the because we are interracting with the UI directly and the
    // thread that this function is running on may not be the UI thread; if a non-UI thread modifies
    // the UI, an exception is thrown

    MainPage::Current->Dispatcher->RunAsync(
        CoreDispatcherPriority::Normal,
        ref new DispatchedHandler([this, buffer]()
        {
            ShowData(
                "Number of interrupt events received: " + numInterruptsReceived.ToString()
                + "\nReceived " + buffer->Length.ToString() + " bytes",
                NotifyType::StatusMessage);
        }));
}
```

## <a name="step-2-get-the-interrupt-pipe-object-interrupt-in"></a>手順 2:割り込みパイプ オブジェクト (割り込み IN) を取得します。


イベント ハンドラーを登録する、 [ **DataReceived** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)イベントへの参照を取得、 [ **UsbInterruptInPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)これらを使用してプロパティ:

-   [**UsbDevice.DefaultInterface.InterruptInPipes\[n\]**  ](https://msdn.microsoft.com/library/windows/apps/dn264292)割り込みエンドポイントが、最初の USB インターフェイスに存在する場合。
-   [**UsbDevice.Configuration.UsbInterfaces\[m\]します。InterruptInPipes\[n\]**  ](https://msdn.microsoft.com/library/windows/apps/dn264292)を列挙するため、デバイスでサポートされているインターフェイスごとのパイプですべて中断します。
-   [**UsbInterface.InterfaceSettings\[m\]します。InterruptInEndpoints \[n\]します。パイプ**](https://msdn.microsoft.com/library/windows/apps/dn264292)インターフェイスの設定で定義されている、割り込みのパイプを列挙するためです。
-   [**UsbEndpointDescriptor.AsInterruptInEndpointDescriptor.Pipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor#Windows_Devices_Usb_UsbInterruptInEndpointDescriptor_Pipe)の割り込みのエンドポイントのエンドポイント記述子からパイプ オブジェクトを取得します。

**注**パイプ オブジェクトを取得して現在選択されていないインターフェイス設定の割り込みのエンドポイントを列挙することによって回避できます。 データを転送するには、パイプがアクティブな設定でエンドポイントを関連付ける必要があります。



## <a name="step-3-register-the-event-handler-to-start-receiving-data-interrupt-in"></a>手順 3:(割り込み IN) のデータの受信を開始するイベント ハンドラーを登録します。


次に、イベント ハンドラーを登録する必要があります、 [ **UsbInterruptInPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)を発生させるオブジェクト、 [ **DataReceived** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)イベント。

このコード例では、イベント ハンドラーを登録する方法を示します。 この例で、クラスをイベント ハンドラーをイベント ハンドラーを登録すると、データの送受信かどうか、パイプは現在のパイプの追跡を保持します。 すべての情報は、次の手順に示すように、イベント ハンドラーの登録を解除するのに使用されます。

```CSharp
private void RegisterForInterruptEvent(TypedEventHandler<UsbInterruptInPipe, UsbInterruptInEventArgs> eventHandler)
{
    // Search for the correct pipe that has the specified endpoint number
    interruptPipe = usbDevice.DefaultInterface.InterruptInPipes[0];

    // Save the interrupt handler so we can use it to unregister
    interruptEventHandler = eventHandler;

    interruptPipe.DataReceived += interruptEventHandler;

    registeredInterruptHandler = true;
}
```

```CSharp
void RegisterForInterruptEvent(TypedEventHandler<UsbInterruptInPipe, UsbInterruptInEventArgs> eventHandler)
    // Search for the correct pipe that has the specified endpoint number
    interruptInPipe = usbDevice.DefaultInterface.InterruptInPipes.GetAt(pipeIndex);

    // Save the token so we can unregister from the event later
    interruptEventHandler = interruptInPipe.DataReceived += eventHandler;

    registeredInterrupt = true;    

}
```

イベント ハンドラーが登録されると、データが関連付けられている割り込みパイプで受信するたびに呼び出されます。

## <a name="step-4-unregister-the-event-handler-to-stop-receiving-data-interrupt-in"></a>手順 4:(割り込み IN) のデータの受信を停止するイベント ハンドラーの登録解除します。


データの受信が完了した後、イベント ハンドラーの登録を解除します。

このコード例では、イベント ハンドラーの登録を解除する方法を示します。 この例で場合は、以前に登録されたイベント ハンドラー メソッドは、追跡対象のイベント ハンドラーを取得し、割り込みパイプで登録を解除します。

```CSharp
private void UnregisterInterruptEventHandler()
{
    if (registeredInterruptHandler)
    {
        interruptPipe.DataReceived -= interruptEventHandler;

        registeredInterruptHandler = false;
    }
}
```

```CSharp
void UnregisterFromInterruptEvent(void)
{
    if (registeredInterrupt)
    {
        interruptInPipe.DataReceived -= eventHandler;

        registeredInterrupt = false;
    }
}
```

イベント ハンドラーを登録解除した後、アプリは、割り込みイベントでは、イベント ハンドラーは呼び出されませんので、割り込みパイプからデータを受信を停止します。 これは、割り込みのパイプには、データの取得を停止するという意味ではありません。