---
Description: UsbInterfaceSetting オブジェクトを使用して、現在の設定を取得し、インターフェイスで設定します。
title: USB インターフェイス設定の選択方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03fb325f51542bb3b6441ecc9170db3f79d6d74a
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419562"
---
# <a name="how-to-select-a-usb-interface-setting-uwp-app"></a>USB インターフェイス設定の選択方法 (UWP アプリ)

このトピックでは、USB インターフェイス内の設定を変更する方法について説明します。 使用して、 [ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)オブジェクトを現在の設定を取得し、インターフェイスで設定します。

## <a name="before-you-start"></a>開始前の作業

- デバイスを開いて、取得する必要がありますが、 [ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト。 読み取り[USB デバイス (UWP アプリ) に接続する方法](how-to-connect-to-a-usb-device--uwp-app-.md)します。
- コード例は、CustomUSBDevice サンプルに基づいています。 完全なサンプルは、このコード ギャラリーのページからダウンロードできます。

## <a name="about-usb-interface-settings"></a>USB インターフェイスの設定について

USB インターフェイスごとにグループ化されている 1 つまたは複数のエンドポイントを公開する*インターフェイス設定*します。 これらの設定はデバイス定義されと呼ばれる番号で識別、*インデックス設定*します。 各インターフェイス*1 つだけ*アクティブな設定です。 複数のインターフェイス デバイスでは、各インターフェイスは、アクティブな設定が必要です。 設定がアクティブな場合は、そのエンドポイントとの間にデータを転送できます。 データ転送は、非アクティブな設定でエンドポイントが無効になります。

設定は、デバイスで選択した後に、アクティブ化すると言います。 既定のアクティブな設定は、インターフェイスの最初の設定です。

各設定は、によって表される、 [ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)オブジェクト。 オブジェクトを使用すると、UWP アプリは、これらの操作を実行できます。

- インターフェイス内のすべての設定を列挙中に特定の設定がアクティブかどうかを確認します。
- 設定を選択する要求を開始します。

USB インターフェイスの設定については、[USB デバイス レイアウト](usb-device-layout.md)を参照してください。

## <a name="get-the-active-setting-of-a-usb-interface"></a>USB インターフェイスのアクティブな設定を取得します。

1. 取得、 [ **UsbInterface** ](https://msdn.microsoft.com/library/windows/apps/dn264121)オブジェクトから取得した前[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)オブジェクト。 このコード例では、USB 構成では、最初のインターフェイスを取得します。 デバイスは、複数インタ フェースを取得できます、 **UsbInterface**オブジェクトのすべてのインターフェイスを列挙することで使用することです。 配列から入手できる、 [ **UsbConfiguration.UsbInterfaces** ](https://msdn.microsoft.com/library/windows/apps/dn263808)プロパティの値。
2. 配列として、インターフェイスで定義されているすべての設定を取得する[ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)オブジェクトを取得することによって、 [ **UsbInterface.InterfaceSettings** ](https://msdn.microsoft.com/library/windows/apps/dn264291)プロパティの値。
3. 配列を列挙し、各イテレーションでチェックして、設定がアクティブかどうかを確認、 [ **UsbInterfaceSetting.Selected** ](https://msdn.microsoft.com/library/windows/apps/dn264285)プロパティ。

このコード例では、既定のインターフェイスで定義されているすべての設定の設定の数を取得する方法を示します。

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

## <a name="set-a-usb-interface-setting"></a>USB インターフェイスを設定します。

現在アクティブでない設定を選択する必要があります、 [ **UsbInterfaceSetting** ](https://msdn.microsoft.com/library/windows/apps/dn264278)オブジェクトを選択し、呼び出すことにより非同期操作を開始する設定を[ **UsbInterfaceSetting.SelectSettingAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264286)メソッド。 操作では、値は返されません。

```CSharp
private async void SetInterfaceSetting(UsbDevice device, Byte settingNumber)
{
    var interfaceSetting = device.DefaultInterface.InterfaceSettings[settingNumber];

    await interfaceSetting.SelectSettingAsync();

    MainPage.Current.NotifyUser("Interface Setting is set to " + settingNumber, NotifyType.StatusMessage);
}
```

# <a name="see-also"></a>関連項目

[**UsbInterfaceSetting.Selected**](https://msdn.microsoft.com/library/windows/apps/dn264285)

[**UsbInterfaceSetting.SelectSettingAsync**](https://msdn.microsoft.com/library/windows/apps/dn264286)
