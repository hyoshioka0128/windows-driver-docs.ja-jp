---
Description: 通常、USB デバイスと通信するアプリは、いくつかのコントロールの転送要求を送信します。
title: USB コントロール転送の送信方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2251863942c5ab21c4fae499603422459930ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360147"
---
# <a name="how-to-send-a-usb-control-transfer-uwp-app"></a>USB コントロール転送の送信方法 (UWP アプリ)


**要約**

-   USB セットアップ パケットを書式設定する方法
-   アプリから USB 制御転送を開始する方法

**重要な API**

-   [**SendControlInTransferAsync**](https://msdn.microsoft.com/library/windows/apps/dn264027)
-   [**SendControlOutTransferAsync**](https://msdn.microsoft.com/library/windows/apps/dn264044)

通常、USB デバイスと通信するアプリは、いくつかのコントロールの転送要求を送信します。 それらの要求では、デバイスに関する情報を取得し、ハードウェア ベンダーによって定義されたコントロールのコマンドを送信します。 このトピックでは、コントロールの転送と書式を設定し、UWP アプリで送信する方法について学習します。

コントロール転送では、読み取り、構成情報の書き込みまたはまたはハードウェア ベンダーによって定義されているデバイスに固有の機能を実行することができます。 アウト転送では; は、転送は、書き込み操作を実行する場合読み取り操作の転送が。 方向に関係なく、ホスト システムで、UWP アプリなど、ソフトウェアは常にビルドし、コントロールの転送要求を開始します。 アプリでは、読み取りまたは書き込みのデータを移動する制御を開始できます。 その場合は、追加のバッファーを送信する必要があります。

コントロールの転送のすべての型に対応する[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)これらのメソッドを提供します。

-   [**SendControlOutTransferAsync (UsbSetupPacket)**](https://msdn.microsoft.com/library/windows/apps/dn264047)
-   [**SendControlInTransferAsync (UsbSetupPacket)**](https://msdn.microsoft.com/library/windows/apps/dn264037)
-   [**SendControlOutTransferAsync (UsbSetupPacket、IBuffer)**](https://msdn.microsoft.com/library/windows/apps/dn264050)
-   [**SendControlInTransferAsync (UsbSetupPacket、IBuffer)**](https://msdn.microsoft.com/library/windows/apps/dn264028)

![windows ランタイム api、usb で usb 制御転送します。](images/scenario2-flowchart.png)

USB 制御転送は、データの記述子を取得または標準のコマンドを送信するも使用されます。 ただし、によって提供される特定のメソッドを呼び出すことによって、これらの種類の要求を送信することは推奨[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)コントロールの転送を手動で構築するのではなく。 たとえば、代替の設定を選択する呼び出し[ **SelectSettingAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264286)呼び出す代わりに[ **SendControlOutTransferAsync (UsbSetupPacket)**](https://msdn.microsoft.com/library/windows/apps/dn264047).

コントロールの転送が特定の標準的な要求の種類がサポートされていません。 ただし、デバイスがでサポートされているデバイスのクラスに属するかどうか[ **Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)クラス、デバイスの仕様で定義されている一部の要求を送信することができます。

## <a name="before-you-start"></a>はじめに...


-   必要がある場合、デバイスを開くし、取得、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト。 読み取り[USB デバイス (UWP アプリ) に接続する方法](how-to-connect-to-a-usb-device--uwp-app-.md)します。
-   コントロールのベンダー定義コマンドに関する情報を取得します。 通常、これらのコマンドは、ハードウェアの仕様で定義されます。
-   Scenario2 CustomUsbDeviceAccess サンプルでは、このトピックに示す完全なコードを確認できます\_ControlTransfer.cpp と Scenario2\_ControlTransfer.h します。

## <a name="step-1-populate-the-setup-packet"></a>手順 1:セットアップのパケットを設定します。


このトピックでは、コントロールの転送をさまざまなパターンでライトが点滅しているデバイスに送信されます。 セットアップのパケットを設定するには、制御コマンドは、ハードウェア ベンダーによって定義されますを知る必要があります。

-   **bmRequestType** (D7)。OUT
-   **bmRequestType** (D4)。デバイス
-   **bmRequestType** (D6.D5):製造元
-   **bRequest**:0x03
-   **wValue**:0 ~ 7 (包括的に、その範囲の任意の数)
-   **wIndex**:0
-   **wLength**:0

コントロールの転送に設定する必要があります、*セットアップ パケット*転送に関するすべての情報を格納している、;、要求が読み取りまたは書き込みデータ、要求の種類、およびにするかどうか。 セットアップのパケットの形式は、公式の USB 仕様で定義されます。 セットアップのパケットのフィールドの値は、デバイスのハードウェアの仕様によって提供されます。

1.  作成、 [ **UsbSetupPacket** ](https://msdn.microsoft.com/library/windows/apps/dn278431)オブジェクト。
2.  設定、 [ **UsbSetupPacket** ](https://msdn.microsoft.com/library/windows/apps/dn278431)さまざまなプロパティを設定するオブジェクト。 次の表は、USB 定義のセットアップ パケット フィールドで、およびそれらのフィールドに対応するプロパティを示します。

    | セクション 9.3 内のフィールド     | プロパティ                                                                              | 説明                                                                                                                                                                                                                            |
    |---------------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **bmRequestType** (D7)    | [**UsbControlRequestType.Direction**](https://msdn.microsoft.com/library/windows/apps/dn263833)      | 要求の方向です。 かどうか、要求は (転送) 内のホストにホストから (転送) をデバイスまたはデバイスには。                                                                                                                 |
    | **bmRequestType** (D4)    | [**UsbControlRequestType.Recipient**](https://msdn.microsoft.com/library/windows/apps/dn263841)      | 要求の受信者。 コントロールのすべての転送は、既定のエンドポイントを対象します。 ただし、デバイス、インターフェイス、エンドポイント、またはその他の受信者があります。 詳細については USB デバイスでは、インターフェイス、エンドポイントの階層では、デバイスのレイアウトを参照してください。 |
    | **bmRequestType** (D6.D5) | [**UsbControlRequestType.ControlTransferType**](https://msdn.microsoft.com/library/windows/apps/dn263829) | 要求のカテゴリ。 Standard、クラス、またはベンダー。                                                                                                                                                                                       |
    | **bRequest**              | [**UsbSetupPacket.Request**](https://msdn.microsoft.com/library/windows/apps/dn278437)                        | 要求の種類。 要求が GET などの標準の要求がかどうか\_記述子の要求、その要求は、USB 仕様によって定義されます。 それ以外の場合、ベンダー定義されている可能性があります。                                                           |
    | **wValue**                | [**UsbSetupPacket.Value**](https://msdn.microsoft.com/library/windows/apps/dn278452)                            | 要求の種類によって異なります。                                                                                                                                                                                                        |
    | **wIndex**                | [**UsbSetupPacket.Index**](https://msdn.microsoft.com/library/windows/apps/dn278433)                            | 要求の種類によって異なります。                                                                                                                                                                                                        |
    | **wLength**               | [**UsbSetupPacket.Length**](https://msdn.microsoft.com/library/windows/apps/dn278435)                          | この要求で送受信されるデータ パケットの長。                                                                                                                                                                            |
**注**特定コントロール転送を提供する必要があります**bmRequestType**生のバイトとして。 その場合は、バイトで設定できる、 [ **UsbControlRequestType.AsByte** ](https://msdn.microsoft.com/library/windows/apps/dn263827)プロパティ。

## <a name="step-2-start-an-asynchronous-operation-to-send-the-control-transfer"></a>手順 2:コントロールの転送を送信する非同期操作を開始します。


コントロールの転送を送信する必要を[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト。 コントロール、転送は、セットアップ パケットに続くデータ パケットは必要ありません。

コントロールの転送を開始するを呼び出すのオーバーライドを[ **SendControlInTransferAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264028)または[ **SendControlOutTransferAsync**](https://msdn.microsoft.com/library/windows/apps/dn264050)します。 データ パケットを転送に使用する場合、呼び出す**SendControlOutTransferAsync (UsbSetupPacket、IBuffer)**、 **SendControlInTransferAsync (UsbSetupPacket、IBuffer)** します。 これらのメソッドは、書き込むデータを格納またはデバイスからデータを受信する追加パラメーターを取得します。 フローチャートを使用すると、上書きを呼び出すかを判断できます。

呼び出しを開始し、非同期操作。 操作が完了、呼び出しから戻る[ **IAsyncOperation** ](https://msdn.microsoft.com/library/windows/desktop/br205802)操作の結果を格納しているオブジェクト。 アウト転送では、オブジェクトは、転送に送信されたバイト数を返します。 転送では、オブジェクトには、デバイスから読み取られたデータを格納しているバッファーが含まれます。

## <a name="usb-control-transfer-code-example"></a>USB 制御転送のコード例


このコード例では、SuperMUTT デバイスで点滅しているパターンを変更するコントロールの転送を送信する方法を示します。 転送のセットアップのパケットには、ベンダー定義コマンドが含まれています。 この例は Scenario2\_ControlTransfer.cpp します。

```ManagedCPlusPlus
async Task SetSuperMuttLedBlinkPatternAsync(Byte pattern)
        {
            UsbSetupPacket initSetupPacket = new UsbSetupPacket
            {
                RequestType = new UsbControlRequestType
                {
                    Direction = UsbTransferDirection.Out,
                    Recipient = UsbControlRecipient.Device,
                    ControlTransferType = UsbControlTransferType.Vendor
                },
                Request = SuperMutt.VendorCommand.SetLedBlinkPattern,
                Value = pattern,
                Length = 0
            };

            UInt32 bytesTransferred = await EventHandlerForDevice.Current.Device.SendControlOutTransferAsync(initSetupPacket);

            MainPage.Current.NotifyUser("The Led blink pattern is set to " + pattern.ToString(), NotifyType.StatusMessage);
        }
```

このコード例では、SuperMUTT デバイスで点滅しているパターンを変更するコントロールの転送を送信する方法を示します。 転送のセットアップのパケットには、ベンダー定義コマンドが含まれています。 この例は Scenario2\_ControlTransfer.cpp します。

```CSharp
async Task<IBuffer> SendVendorControlTransferInToDeviceRecipientAsync(Byte vendorCommand, UInt32 dataPacketLength)
 {
    // Data will be written to this buffer when we receive it
    var buffer = new Windows.Storage.Streams.Buffer(dataPacketLength);

    UsbSetupPacket initSetupPacket = new UsbSetupPacket
    {
        RequestType = new UsbControlRequestType
        {
            Direction = UsbTransferDirection.In,
            Recipient = UsbControlRecipient.Device,
            ControlTransferType = UsbControlTransferType.Vendor,
        },
        Request = vendorCommand,
        Length = dataPacketLength
    };

    return await EventHandlerForDevice.Current.Device.SendControlInTransferAsync(initSetupPacket, buffer);
}
```








