---
Description: UsbInterfaceSetting オブジェクトを使用して現在の設定を取得し、インターフェイスで設定を設定します。
title: USB インターフェイス設定の選択方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a4fa1e7c1a1f1dfb66b7e710ef59a44545b5637
ms.sourcegitcommit: 7c64faf8aa00d064efc39ab3c08c6ade8944c740
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72776563"
---
# <a name="how-to-select-a-usb-interface-setting-uwp-app"></a>USB インターフェイス設定の選択方法 (UWP アプリ)

このトピックでは、USB インターフェイス内の設定の変更について説明します。 [**Usbinterfacesetting**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)オブジェクトを使用して現在の設定を取得し、インターフェイスの設定を設定します。

## <a name="before-you-start"></a>開始前の作業

- デバイスを開いて、 [**usbdevice**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)オブジェクトを取得しておく必要があります。 「 [USB デバイスに接続する方法 (UWP アプリ)](how-to-connect-to-a-usb-device--uwp-app-.md)」を参照してください。
- コード例は、CustomUSBDevice サンプルを基にしています。 完全なサンプルは、このコードギャラリーページからダウンロードできます。

## <a name="about-usb-interface-settings"></a>USB インターフェイスの設定について

各 USB インターフェイスは、*インターフェイスの設定*でグループ化された1つ以上のエンドポイントを公開します。 これらの設定はデバイスで定義され、*設定インデックス*と呼ばれる番号で識別されます。 各インターフェイスには、アクティブな設定が*1 つだけ*必要です。 複数のインターフェイスデバイスの場合、各インターフェイスにはアクティブな設定が必要です。 設定がアクティブな場合は、エンドポイントとの間でデータを転送できます。 非アクティブな設定のエンドポイントは、データ転送に対して無効になっています。

設定は、デバイス上で選択された後に "アクティブ" と呼ばれます。 既定の [アクティブ] 設定は、インターフェイスの最初の設定です。

各設定は、 [**Usbinterfacesetting**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)オブジェクトによって表されます。 オブジェクトを使用することによって、UWP アプリは次の操作を実行できます。

- インターフェイスのすべての設定を列挙しながら、特定の設定がアクティブかどうかを判断します。
- 設定を選択する要求を開始します。

USB インターフェイスの設定の詳細については、「 [usb デバイスのレイアウト](usb-device-layout.md)」を参照してください。

## <a name="get-the-active-setting-of-a-usb-interface"></a>USB インターフェイスのアクティブな設定を取得する

1. 以前に取得した[**Usbinterface**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)オブジェクトから[**usbinterface**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface)オブジェクトを取得します。 このコード例では、USB 構成の最初のインターフェイスを取得します。 複数のインターフェイスを持つデバイスの場合は、すべてのインターフェイスを列挙することによって、使用する**usbinterface**オブジェクトを取得できます。 この配列は、 [**Usbconfiguration. Usbconfiguration**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_UsbInterfaces)プロパティ値を使用して取得できます。
2. [**Usbinterface. InterfaceSettings**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_InterfaceSettings)プロパティ値を取得して、インターフェイスに定義されているすべての設定を[**usbinterfacesetting**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)オブジェクトの配列として取得します。
3. 配列を列挙し、各繰り返しで、設定がアクティブかどうかを確認するために、 [**Usbinterfacesetting. Selected**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Selected)プロパティをチェックします。

このコード例は、既定のインターフェイスで定義されているすべての設定の設定番号を取得する方法を示しています。

```CSharp
void GetInterfaceSetting (UsbDevice device)
{
        auto interfaceSettings = device.InterfaceSettings;

        for each(UsbInterfaceSetting interfaceSetting in interfaceSettings)
        {
            if (interfaceSetting->Selected)
            {
                uint8 interfaceSettingNumber = interfaceSetting.InterfaceDescriptor.AlternateSettingNumber;

                // Use the interface setting number. Not shown.

                break;
            }
        }
}
```

## <a name="set-a-usb-interface-setting"></a>USB インターフェイス設定の設定

現在アクティブになっていない設定を選択するには、設定の[**usbinterfacesetting**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)オブジェクトを検索してから、 [**Usbinterfacesetting. selectsettingasync**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync)メソッドを呼び出して非同期操作を開始する必要があります。 操作は値を返しません。

```CSharp
private async void SetInterfaceSetting(UsbDevice device, Byte settingNumber)
{
    var interfaceSetting = device.DefaultInterface.InterfaceSettings[settingNumber];

    await interfaceSetting.SelectSettingAsync();

    MainPage.Current.NotifyUser("Interface Setting is set to " + settingNumber, NotifyType.StatusMessage);
}
```

## <a name="see-also"></a>参照

[**UsbInterfaceSetting を選択しました。** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Selected)

[**UsbInterfaceSetting. SelectSettingAsync**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync)
