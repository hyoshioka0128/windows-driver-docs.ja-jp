---
Description: に関する情報の取得、USB デバイスとの対話の主なタスクの 1 つです。
title: USB 記述子の取得方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d18df5103cc11a300748a3070e212b015dd38b79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364807"
---
# <a name="how-to-get-usb-descriptors-uwp-app"></a>USB 記述子の取得方法 (UWP アプリ)


**概要**

-   USB デバイスのレイアウトを理解します。
-   標準の USB 記述子を取得します。
-   カスタムの記述子を取得します。

**重要な API**

-   [**UsbDeviceDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn263961)
-   [**UsbConfigurationDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297689)
-   [**UsbDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn263863)

に関する情報の取得、USB デバイスとの対話の主なタスクの 1 つです。 すべての USB デバイスは、記述子と呼ばれるデータ構造がいくつかの形式で情報を提供します。 このトピックでは、UWP アプリがエンドポイント、インターフェイス、構成、およびデバイス レベルのデバイスから記述子を取得する方法について説明します。

## <a name="usb-descriptors"></a>USB 記述子


USB デバイスが 2 つの主な記述子では、その機能について説明します。 デバイス記述子および構成記述子。

USB デバイスを提供する必要があります、*デバイス記述子*全体として、USB デバイスに関する情報を格納します。 デバイスは、その記述子を提供していないか、形式が正しくない記述子を提供する場合の Windows は、デバイス ドライバーを読み込むことはできません。 記述子の最も重要な情報は、デバイスの*ハードウェア ID*デバイス (の組み合わせ**ベンダー ID**と**製品 ID**フィールド)。 Windows デバイス用のインボックス ドライバーと一致することがその情報に基づいています。 キーは、別の情報は、*最大パケット サイズ*の既定のエンドポイント (**MaxPacketSize0**)。 既定のエンドポイントは、すべてのコントロールのターゲットは、ホストがそれを構成するデバイスに送信を要求します。

デバイス記述子の長さは固定されています。

USB デバイスを完全なも提供する必要があります*構成記述子*します。 この記述子の開始部分が 9 バイトの長さを固定、残りの部分は可変長インターフェイスとエンドポイントの数によってはそれらのインターフェイスをサポートします。 固定長の部分は、USB 構成に関する情報を提供します。 数インターフェイス サポートと電力消費量と、デバイスはその構成します。 その最初の 9 バイトには、すべての USB インターフェイスに関する情報を提供する記述子の可変部分が続きます。 各インターフェイスは 1 つまたは複数のインターフェイスの設定と各設定は、一連のエンドポイントの構成されます。 可変部分では、インターフェイス、代替の設定、およびエンドポイントの記述子が含まれます。

デバイスのレイアウトに関する詳細については、次を参照してください。[標準の USB ディスクリプター](standard-usb-descriptors.md)します。

## <a name="before-you-start"></a>はじめに...


-   デバイスを開いて、取得する必要がありますが、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト。 読み取り[USB デバイス (UWP アプリ) に接続する方法](how-to-connect-to-a-usb-device--uwp-app-.md)します。
-   Scenario5 CustomUsbDeviceAccess サンプルでは、このトピックに示す完全なコードを確認できます\_UsbDescriptors ファイル。
-   デバイスのレイアウトに関する情報を取得します。 **Usbview.exe**アプリケーションを使用するすべての USB コント ローラーとそれらに接続されている USB デバイスを指定するには (Windows 8 用 Windows ソフトウェア開発キット (SDK) に含まれています)。 接続された各デバイスのデバイス、構成、インターフェイス、およびデバイスの機能について理解するためのエンドポイント記述子を表示できます。

## <a name="how-to-get-the-device-descriptor"></a>デバイス記述子を取得する方法


UWP アプリから、以前に取得したデバイス記述子を取得できます[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクトを取得することによって、 [ **UsbDevice.DeviceDescriptor** ](https://msdn.microsoft.com/library/windows/apps/dn264002)プロパティの値。

このコード例では、デバイスの記述子からフィールド値を含む文字列を設定する方法を示します。

```CSharp
String GetDeviceDescriptorAsString (UsbDevice device)
{
    String content = null;

    var deviceDescriptor = device.DeviceDescriptor;

    content = "Device Descriptor\n"
            + "\nUsb Spec Number : 0x" + deviceDescriptor.BcdUsb.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nMax Packet Size (Endpoint 0) : " + deviceDescriptor.MaxPacketSize0.ToString("D", NumberFormatInfo.InvariantInfo)
            + "\nVendor ID : 0x" + deviceDescriptor.IdVendor.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nProduct ID : 0x" + deviceDescriptor.IdProduct.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nDevice Revision : 0x" + deviceDescriptor.BcdDeviceRevision.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nNumber of Configurations : " + deviceDescriptor.NumberOfConfigurations.ToString("D", NumberFormatInfo.InvariantInfo);
    
    return content;
}
```

出力は次のように表示されます。

![usb デバイス記述子](images/device-descriptors-app.png)

## <a name="how-to-get-the-configuration-descriptor"></a>構成記述子を取得する方法


以前に取得した構成記述子の固定部分を取得する[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト

1.  取得、 [ **UsbConfiguration** ](https://msdn.microsoft.com/library/windows/apps/dn297681)オブジェクトから[ **UsbDevice**](https://msdn.microsoft.com/library/windows/apps/dn263883)します。 **UsbConfiguration**デバイスによって定義されている最初の USB 構成を表し、基になるデバイス ドライバーによっても既定で選択されます。
2.  取得、 [ **UsbConfiguration.ConfigurationDescriptor** ](https://msdn.microsoft.com/library/windows/apps/dn263799)プロパティの値。

構成記述子の固定部分では、デバイスの電源の特性を示します。 たとえば、デバイスがバスまたは外部ソースから電力を消費しているかどうかを確認できます (を参照してください[ **UsbConfigurationDescriptor.SelfPowered**](https://msdn.microsoft.com/library/windows/apps/dn263787))。 デバイスは、バスから電力を消費するが場合、(milliamp 単位) でどれくらいの電力を消費 (を参照してください[ **UsbConfigurationDescriptor.MaxPowerMilliamps**](https://msdn.microsoft.com/library/windows/apps/dn297702))。 デバイスが取得することでそれ自体または低電力状態からシステムをスリープ解除できるかどうかを判断することも、 [ **UsbConfigurationDescriptor.RemoteWakeup** ](https://msdn.microsoft.com/library/windows/apps/dn263785)値。

このコード例では、文字列で構成記述子の固定部分を取得する方法を示します。

```CSharp
String GetConfigurationDescriptorAsString(UsbDevice device)
{
    String content = null;

    var usbConfiguration = device.Configuration;
    var configurationDescriptor = usbConfiguration.ConfigurationDescriptor;

    content = "Configuration Descriptor\n"
            + "\nNumber of Interfaces : " + usbConfiguration.UsbInterfaces.Count.ToString("D", NumberFormatInfo.InvariantInfo)
            + "\nConfiguration Value : 0x" + configurationDescriptor.ConfigurationValue.ToString("X2", NumberFormatInfo.InvariantInfo)
            + "\nSelf Powered : " + configurationDescriptor.SelfPowered.ToString()
            + "\nRemote Wakeup : " + configurationDescriptor.RemoteWakeup.ToString()
            + "\nMax Power (milliAmps) : " + configurationDescriptor.MaxPowerMilliamps.ToString("D", NumberFormatInfo.InvariantInfo);

    return content;
}
```

出力は次のように表示されます。

![usb 構成記述子](images/config-desc-app.png)

## <a name="how-to-get-interface-descriptors"></a>インターフェイスの記述子を取得する方法


次に、構成の一部である USB インターフェイスに関する情報を取得できます。

USB インターフェイスは、インターフェイスの設定のコレクションです。 そのため、全体のインターフェイスを記述する記述子ではありません。 用語*インターフェイス記述子*インターフェイス内の設定を表すデータ構造を示します。

[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)名前空間が各 USB インターフェイスに関する情報の取得に使用できるオブジェクトを公開し、そのインターフェイスに含まれる (代替の設定) の記述子をインターフェイスのすべて。 構成記述子の可変長の部分からの記述子。

インターフェイスの記述子を取得する[ **UsbConfiguration**](https://msdn.microsoft.com/library/windows/apps/dn297681)、

1.  取得することによって、構成内でインターフェイスの配列を取得、 [ **UsbConfiguration.UsbInterfaces** ](https://msdn.microsoft.com/library/windows/apps/dn263808)プロパティ。
2.  各インターフェイスに対して ([**UsbInterface**](https://msdn.microsoft.com/library/windows/apps/dn264121))、この情報を取得します。
    -   アクティブとデータを転送できる一括と割り込みパイプします。
    -   インターフェイスで代替の設定の配列。
    -   インターフェイスの記述子の配列。

このコード例をすべて取得[ **UsbInterface** ](https://msdn.microsoft.com/library/windows/apps/dn264121)構成オブジェクト。 各オブジェクトは、ヘルパー メソッドは、代替の設定と開いている一括とインターフェイスのパイプの数を取得します。 デバイスは、複数のインターフェイスをサポートする場合は、デバイス クラスやサブクラスでは、各インターフェイスのプロトコルのコードが異なることができます。 ただし、代替の設定のすべてのインターフェイス記述子では、同じコードを指定する必要があります。 この例では、メソッドは、インターフェイス全体のコードを調べるには、最初の設定のインターフェイスの記述子からデバイス クラスやサブクラスでは、プロトコルのコードを取得します。

```CSharp
String GetInterfaceDescriptorsAsString(UsbDevice device)
{
    String content = null;
    
    var interfaces = device.Configuration.UsbInterfaces;

    content = "Interface Descriptors";

        foreach (UsbInterface usbInterface in interfaces)
        {
            // Class/subclass/protocol values from the first interface setting.

            UsbInterfaceDescriptor usbInterfaceDescriptor = usbInterface.InterfaceSettings[0].InterfaceDescriptor;

            content +="\n\nInterface Number: 0x" +usbInterface.InterfaceNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nClass Code: 0x" +usbInterfaceDescriptor.ClassCode.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nSubclass Code: 0x" +usbInterfaceDescriptor.SubclassCode.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nProtocol Code: 0x" +usbInterfaceDescriptor.ProtocolCode.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of Interface Settings: "+usbInterface.InterfaceSettings.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Bulk In pipes: "+usbInterface.BulkInPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Bulk Out pipes: "+usbInterface.BulkOutPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Interrupt In pipes: "+usbInterface.InterruptInPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Interrupt Out pipes: "+usbInterface.InterruptOutPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo);
       }

    return content;
}
```

出力は次のように表示されます。

![usb インターフェイス記述子](images/interface-desc-app.png)

## <a name="how-to-get-endpoint-descriptors"></a>エンドポイントの記述子を取得する方法


(既定のコントロール エンドポイント) を除くすべての USB エンドポイントには、エンドポイントの記述子が必要です。 特定のエンドポイントのエンドポイント記述子を取得するインターフェイスし、代替を知る必要があります、エンドポイントが属するに設定します。

1.  取得、 [ **UsbInterface** ](https://msdn.microsoft.com/library/windows/apps/dn264121)エンドポイントを格納するオブジェクト。
2.  取得することで別の設定の配列を取得する[ **UsbInterface.InterfaceSettings**](https://msdn.microsoft.com/library/windows/apps/dn264291)します。
3.  を、配列内で設定を見つけます ([**UsbInterfaceSetting**](https://msdn.microsoft.com/library/windows/apps/dn264278)) エンドポイントを使用します。
4.  各設定内で一括および割り込みの記述子の配列を列挙することによって、エンドポイントが見つかりません。

    エンドポイントの記述子は、これらのオブジェクトによって表されます。

    -   [**UsbBulkInEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297543)
    -   [**UsbBulkOutEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297619)
    -   [**UsbInterruptInEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn264294)
    -   [**UsbInterruptOutEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn278420)

使用することができます、デバイスに 1 つだけのインターフェイスがある場合、 [ **UsbDevice.DefaultInterface** ](https://msdn.microsoft.com/library/windows/apps/dn263998)のコード例で示すようにインターフェイスを取得します。 ここでは、ヘルパー メソッドの取得は、パイプのアクティブなインターフェイスの設定に関連付けられているエンドポイント記述子文字列を設定します。

```CSharp
private String GetEndpointDescriptorsAsString(UsbDevice device)
{
    String content = null;

    var usbInterface = device.DefaultInterface;
    var bulkInPipes = usbInterface.BulkInPipes;
    var bulkOutPipes = usbInterface.BulkOutPipes;
    var interruptInPipes = usbInterface.InterruptInPipes;
    var interruptOutPipes = usbInterface.InterruptOutPipes;

    content = "Endpoint Descriptors for open pipes";

    // Print Bulk In Endpoint descriptors
    foreach (UsbBulkInPipe bulkInPipe in bulkInPipes)
    {
        var endpointDescriptor = bulkInPipe.EndpointDescriptor;

        content +="\n\nBulk In Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
    }

    // Print Bulk Out Endpoint descriptors
    foreach (UsbBulkOutPipe bulkOutPipe in bulkOutPipes)
    {
        var endpointDescriptor = bulkOutPipe.EndpointDescriptor;

        content +="\n\nBulk Out Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
    }

    // Print Interrupt In Endpoint descriptors
    foreach (UsbInterruptInPipe interruptInPipe in interruptInPipes)
    {
        var endpointDescriptor = interruptInPipe.EndpointDescriptor;

        content +="\n\nInterrupt In Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
                + "\nInterval : " + endpointDescriptor.Interval.Duration.ToString();
    }

    // Print Interrupt Out Endpoint descriptors
    foreach (UsbInterruptOutPipe interruptOutPipe in interruptOutPipes)
    {
        var endpointDescriptor = interruptOutPipe.EndpointDescriptor;

        content +="\n\nInterrupt Out Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
                + "\nInterval : " + endpointDescriptor.Interval.Duration.ToString();
    }

    return content;
}
```

出力は次のように表示されます。

![usb エンドポイント記述子](images/endpoint-desc-app.png)

## <a name="how-to-get-custom-descriptors"></a>カスタムの記述子を取得する方法


注意[ **UsbConfiguration**](https://msdn.microsoft.com/library/windows/apps/dn297681)、 [ **UsbInterface**](https://msdn.microsoft.com/library/windows/apps/dn264121)、および[ **UsbInterfaceSetting**](https://msdn.microsoft.com/library/windows/apps/dn264278)という名前のプロパティを公開の各オブジェクト、**記述子**します。 プロパティの値がによって表される記述子の配列を取得する[ **UsbDescriptor** ](https://msdn.microsoft.com/library/windows/apps/dn263863)オブジェクト。 **UsbDescriptor**オブジェクト バッファー記述子のデータを取得するアプリを使用できます。 [**UsbDescriptor.DescriptorType** ](https://msdn.microsoft.com/library/windows/apps/dn263870)と[ **UsbDescriptor.Length** ](https://msdn.microsoft.com/library/windows/apps/dn263874)プロパティ型と記述子を保持するために必要なバッファーの長さを格納します。

**注**  型と長さ、記述子の記述子のすべてのバッファーの最初の 2 バイトも示します。

 

たとえば、 [ **UsbConfiguration.Descriptors** ](https://msdn.microsoft.com/library/windows/apps/dn264289)プロパティは、完全な構成記述子 (固定および可変長の部分) の配列を取得します。 その配列の最初の要素は、固定長の構成記述子 (同じ[ **UsbConfigurationDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297689))、2 番目の要素は、代替の最初の設定のインターフェイスの記述子などなど。

同様に、 [ **UsbInterface.Descriptors** ](https://msdn.microsoft.com/library/windows/apps/dn264289)プロパティは、すべてのインターフェイス記述子および関連するエンドポイント記述子の配列を取得します。 [ **UsbInterfaceSetting.Descriptors** ](https://msdn.microsoft.com/library/windows/apps/dn264281)プロパティは、エンドポイント記述子など、その設定のすべての記述子の配列を取得します。

この記述子を取得する方法は、アプリのカスタム記述子または SuperSpeed デバイス向けエンドポイント コンパニオンの記述子などの他の記述子を取得する必要がある場合に便利です。

このコード例では、構成記述子からバッファー記述子のデータを取得する方法を示します。 例では、記述子の設定を取得し、そのセットに含まれるすべての記述子を解析します。 各の記述子の DataReader オブジェクトを使用して、バッファーを読み取るし、記述子の長さと型を表示します。 この例で示すように、カスタムの記述子を取得できます。

```CSharp
private String GetCustomDescriptorsAsString(UsbDevice device)
{
    String content = null;
    // Descriptor information will be appended to this string and then printed to UI
    content = "Raw Descriptors";

    var configuration = device.Configuration;
    var allRawDescriptors = configuration.Descriptors;

    // Print first 2 bytes of all descriptors within the configuration descriptor    
    // because the first 2 bytes are always length and descriptor type
    // the UsbDescriptor's DescriptorType and Length properties, but we will not use these properties
    // in order to demonstrate ReadDescriptorBuffer() and how to parse it.

    foreach (UsbDescriptor descriptor in allRawDescriptors)
    {
        var descriptorBuffer = new Windows.Storage.Streams.Buffer(descriptor.Length);
        descriptor.ReadDescriptorBuffer(descriptorBuffer);

        DataReader reader = DataReader.FromBuffer(descriptorBuffer);

        // USB data is Little Endian according to the USB spec.
        reader.ByteOrder = ByteOrder.LittleEndian;

        // ReadByte has a side effect where it consumes the current byte, so the next ReadByte will read the next character.
        // Putting multiple ReadByte() on the same line (same variable assignment) may cause the bytes to be read out of order.
        var length = reader.ReadByte().ToString("D", NumberFormatInfo.InvariantInfo);
        var type = "0x" + reader.ReadByte().ToString("X2", NumberFormatInfo.InvariantInfo);

        content += "\n\nDescriptor"
                + "\nLength : " + length
                + "\nDescriptorType : " + type;
    }

    return content;
}
```

 

 




