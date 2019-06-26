---
title: UMDF 1.x ドライバーでの USB デバイスの操作
description: UMDF 1.x ドライバーでの USB デバイスの操作
ms.assetid: 144898a2-c4e1-495f-a6ca-72d9f09bda90
keywords:
- UMDF WDK、USB デバイス
- ユーザー モード ドライバー フレームワーク WDK、USB デバイス
- ユーザー モード ドライバー WDK UMDF、USB デバイス
- WDK UMDF の USB デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89b7b0bb17739bdb397d8c4c7f50f818aa426d0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383979"
---
# <a name="working-with-usb-devices-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでの USB デバイスの操作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、フレームワークの USB デバイス オブジェクトとして各 USB デバイスを表します。 UMDF ドライバーは、ドライバーが USB I/O ターゲット フレームワークのサポートにアクセスできる前に、フレームワークの USB デバイス オブジェクトを作成する必要があります。 UMDF は、UMDF ドライバーを有効にする USB デバイス オブジェクトのメソッドを提供します。

-   [UMDF USB デバイス オブジェクトを作成します。](#creating-a-umdf-usb-device-object)

-   [デバイス情報を取得します。](#obtaining-umdf-usb-device-information)

-   [コントロールの転送を送信します。](#send-a-control-transfer-to-a-umdf-usb-device-object)

-   [電源ポリシーの設定](#set-power-policy-for-a-umdf-usb-device-object)

### <a name="creating-a-umdf-usb-device-object"></a>UMDF USB デバイス オブジェクトを作成します。

フレームワークの USB I/O ターゲット機能を使用する UMDF ドライバーを入手へのポインター、 [IWDFUsbTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetfactory)インターフェイス。 ポインターを取得するには、ドライバーを呼び出す必要があります、 **QueryInterface**メソッド、デバイスの[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)インターフェイス。 次のコード例は、呼び出す方法を示しています。 **QueryInterface**ポインターを取得します。

```cpp
hr = pdevice->QueryInterface(IID_IWDFUsbTargetFactory, (LPVOID*)&ppUsbTargetFactory);
```

ドライバーが次に呼び出す必要があります、 [ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)デバイスの USB I/O ターゲット オブジェクトを作成します。 ドライバーが USB I/O ターゲットを作成した後、ドライバーは、I/O ターゲットに要求を送信できます。 通常、ドライバー呼び出し**IWDFUsbTargetFactory::CreateUsbTargetDevice**内から、 [ **IPnpCallbackHardware::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)コールバック関数。

ドライバーの呼び出し後**IWDFUsbTargetFactory::CreateUsbTargetDevice**、ドライバーは[USB デバイスの情報を取得](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices-in-umdf-1-x-drivers#obtaining-umdf-usb-device-information)(たとえば、USB ディスクリプター デバイス、USB インターフェイス、およびインターフェイスエンドポイントの場合)。 USB 記述子は、USB 仕様で説明します。

### <a name="obtaining-umdf-usb-device-information"></a>UMDF USB デバイスの情報を取得します。

UMDF ドライバーを呼び出してから、 [ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice) UMDF USB ターゲット デバイスを作成するメソッドがオブジェクト、ドライバーは、USB デバイスを対象とする、次のメソッドを呼び出すことができますUSB デバイスに関する情報を取得するためにオブジェクトを定義します。

<a href="" id="iwdfusbtargetdevice--retrievedescriptor"></a>[**IWDFUsbTargetDevice::RetrieveDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)  
デバイスの USB デバイスの記述子を取得します。

<a href="" id="iwdfusbtargetdevice--getnuminterfaces"></a>[**IWDFUsbTargetDevice::GetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)  
デバイスをサポートする USB インターフェイスの数を取得します。

<a href="" id="iwdfusbtargetdevice--retrieveusbinterface"></a>[**IWDFUsbTargetDevice::RetrieveUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)  
ポインターを取得、 [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)いずれかのデバイスをサポートする USB インターフェイスを公開するインターフェイス。

<a href="" id="iwdfusbtargetdevice--retrievedeviceinformation"></a>[**IWDFUsbTargetDevice::RetrieveDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedeviceinformation)  
USB デバイスに関連付けられている機能の情報を取得します。

<a href="" id="iwdfusbtargetdevice--retrievepowerpolicy"></a>[**IWDFUsbTargetDevice::RetrievePowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievepowerpolicy)  
WinUsb 電源ポリシーを取得します。

<a href="" id="iwdfusbtargetdevice--getwinusbhandle"></a>[**IWDFUsbTargetDevice::GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle)  
I/O のターゲット デバイス オブジェクトに関連付けられている WinUsb インターフェイスのハンドルを取得します。

### <a href="" id="send-a-control-transfer-to-a-umdf-usb-device-object"></a>UMDF USB デバイス オブジェクトをコントロールの転送を送信します。

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbTargetDevice::FormatRequestForControlTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer) standard では、デバイスにクラスに固有の説明する I/O 要求の書式を指定するメソッドまたはベンダー固有の USBコントロールの転送。 ドライバーを呼び出して、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)同期または非同期要求を送信するメソッド。

### <a href="" id="set-power-policy-for-a-umdf-usb-device-object"></a>UMDF USB デバイスの電源ポリシーの設定

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbTargetDevice::SetPowerPolicy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy) USB デバイス WinUsb によって使用される電源ポリシーを設定します。 USB デバイスの電源ポリシー効果の変更、デバイスの電源管理の状態にします。

 

 





