---
title: USB インターフェイスの使用
description: USB インターフェイスの使用
ms.assetid: 6a1801e4-bd46-4a78-8c30-7dc62e41a37a
keywords:
- USB i/o ターゲット WDK KMDF、USB インターフェイス
- USB インターフェイス WDK KMDF
- フレームワークオブジェクト WDK KMDF、USB インターフェイスオブジェクト
- インターフェイスオブジェクト WDK KMDF
- 代替の USB インターフェイス設定 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03e3a3578167f44d7fb55f97d0c0b5152058d70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823504"
---
# <a name="working-with-usb-interfaces"></a>USB インターフェイスの使用


フレームワークは、各 USB インターフェイスを*フレームワークの usb インターフェイスオブジェクト*として表します。 ドライバーが[フレームワークの usb デバイスオブジェクトを作成](working-with-usb-devices.md#creating-a-framework-usb-device-object)すると、フレームワークは、デバイスの最初の usb 構成に含まれる各 usb インターフェイスに対してフレームワークの usb インターフェイスオブジェクトを作成します。

ほとんどの USB デバイスにはインターフェイスが1つだけあり、インターフェイスには代替設定が1つだけあります。 通常、このようなデバイスのドライバーは、フレームワークの USB インターフェイスオブジェクトが定義するオブジェクトメソッドを使用する必要はありません。

ドライバーが複数のインターフェイスまたは代替設定を提供する USB デバイスをサポートしている場合、インターフェイスオブジェクトのメソッドを使用すると、ドライバーは次の操作を実行できます。

-   [インターフェイス情報を取得します。](#obtaining-interface-information)

-   [USB インターフェイスの別の設定を選択してください。](#selecting-an-alternate-setting-for-a-usb-interface)

### <a href="" id="obtaining-interface-information"></a>インターフェイス情報の取得

ドライバーが[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出した後、 [**WdfUsbTargetDeviceGetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)を呼び出して、デバイスの usb インターフェイスの1つを表すフレームワークの usb インターフェイスオブジェクトへのハンドルを取得できます。 次に、ドライバーは、usb インターフェイスに関する情報を取得するために、USB インターフェイスオブジェクトが定義するいくつかのメソッドを呼び出すことができます。

ドライバーは、 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出した後、いつでも次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbinterfacegetinterfacenumber--------"></a>[**WdfUsbInterfaceGetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetinterfacenumber)  
USB インターフェイスオブジェクトに関連付けられている USB インターフェイス番号を返します。

<a href="" id="---------wdfusbinterfacegetdescriptor--------"></a>[**WdfUsbInterfaceGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)  
USB インターフェイスの代替設定の1つに関連付けられている USB インターフェイス記述子を取得します。

<a href="" id="---------wdfusbinterfacegetnumendpoints--------"></a>[**WdfUsbInterfaceGetNumEndpoints**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumendpoints)  
USB インターフェイスの代替設定の1つに関連付けられているエンドポイントの数を返します。

<a href="" id="---------wdfusbinterfacegetendpointinformation--------"></a>[**WdfUsbInterfaceGetEndpointInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetendpointinformation)  
エンドポイントとそれに関連付けられているパイプに関する情報を取得します。

ドライバーは、 [**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)を呼び出した後、次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbinterfacegetconfiguredsettingindex--------"></a>[**WdfUsbInterfaceGetConfiguredSettingIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredsettingindex)  
USB インターフェイスに対して現在選択されている別の設定を識別するインデックス値を返します。

<a href="" id="---------wdfusbinterfacegetnumconfiguredpipes--------"></a>[**WdfUsbInterfaceGetNumConfiguredPipes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes)  
指定された USB デバイスインターフェイスに対して構成されているパイプの数を返します。

<a href="" id="---------wdfusbinterfacegetconfiguredpipe--------"></a>[**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)  
指定した USB デバイスインターフェイスとパイプインデックスに関連付けられているフレームワークパイプオブジェクトへのハンドルを返します。

### <a href="" id="selecting-an-alternate-setting-for-a-usb-interface"></a>USB インターフェイスの別の設定を選択する

ドライバーが[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出した後、ドライバーは[**WdfUsbInterfaceGetNumSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumsettings)を呼び出して、USB インターフェイスがサポートする代替設定の数を取得できます。

ドライバーが[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)を呼び出して usb デバイスの構成を選択すると、ドライバーは[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)を呼び出して、構成のいずれかの usb インターフェイスに対して別の設定を選択できます。

デバイスの代替設定には、ゼロから始まる番号を連続して指定する必要があります。

関連情報については、「 [USB インターフェイスで別の設定を選択する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)」を参照してください。

 

 





