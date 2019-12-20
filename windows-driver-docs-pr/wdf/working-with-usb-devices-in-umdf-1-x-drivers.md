---
title: UMDF 1.x ドライバーでの USB デバイスの操作
description: UMDF 1.x ドライバーでの USB デバイスの操作
ms.assetid: 144898a2-c4e1-495f-a6ca-72d9f09bda90
keywords:
- UMDF WDK、USB デバイス
- ユーザーモードドライバーフレームワーク WDK、USB デバイス
- ユーザーモードドライバー WDK UMDF、USB デバイス
- USB デバイス WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 099486de52e0fba166c2d5eea174c8881780e39f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210838"
---
# <a name="working-with-usb-devices-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでの USB デバイスの操作


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークは、各 USB デバイスをフレームワークの USB デバイスオブジェクトとして表します。 UMDF ドライバーは、ドライバーが USB i/o ターゲットに対するフレームワークのサポートにアクセスする前に、フレームワークの USB デバイスオブジェクトを作成する必要があります。 UMDF には、UMDF ドライバーが次のことを行うための USB デバイスオブジェクトメソッドが用意されています。

-   [UMDF USB デバイスオブジェクトを作成する](#creating-a-umdf-usb-device-object)

-   [デバイス情報の取得](#obtaining-umdf-usb-device-information)

-   [制御転送を送信する](#send-a-control-transfer-to-a-umdf-usb-device-object)

-   [電源ポリシーの設定](#set-power-policy-for-a-umdf-usb-device-object)

### <a name="creating-a-umdf-usb-device-object"></a>UMDF USB デバイスオブジェクトの作成

フレームワークの USB i/o ターゲット機能を使用するには、まず、UMDF ドライバーが[IWDFUsbTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetfactory)インターフェイスへのポインターを取得する必要があります。 ポインターを取得するには、ドライバーはデバイスの[Iwdfdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスの**QueryInterface**メソッドを呼び出す必要があります。 次のコード例は、 **QueryInterface**を呼び出してポインターを取得する方法を示しています。

```cpp
hr = pdevice->QueryInterface(IID_IWDFUsbTargetFactory, (LPVOID*)&ppUsbTargetFactory);
```

次に、ドライバーは[**IWDFUsbTargetFactory:: CreateUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)メソッドを呼び出して、デバイスの USB i/o ターゲットオブジェクトを作成する必要があります。 ドライバーは、USB i/o ターゲットを作成した後、i/o ターゲットに要求を送信できます。 通常、ドライバーは、 [**IPnpCallbackHardware:: OnIWDFUsbTargetFactory ハードウェア**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)コールバック関数内から **:: CreateUsbTargetDevice**を呼び出します。

ドライバーが**IWDFUsbTargetFactory:: CreateUsbTargetDevice**を呼び出すと、ドライバーは[usb デバイス情報](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices-in-umdf-1-x-drivers#obtaining-umdf-usb-device-information)(デバイスの usb 記述子、usb インターフェイス、およびインターフェイスエンドポイントなど) を取得できます。 Usb 記述子については、USB 仕様で説明されています。

### <a name="obtaining-umdf-usb-device-information"></a>UMDF USB デバイス情報の取得

UMDF ドライバーは、 [**IWDFUsbTargetFactory:: CreateUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetfactory-createusbtargetdevice)メソッドを呼び出して、umdf usb ターゲットデバイスオブジェクトを作成した後、usb ターゲットデバイスオブジェクトが usb デバイスに関する情報を取得するために定義する次のメソッドを呼び出すことができます。

<a href="" id="iwdfusbtargetdevice--retrievedescriptor"></a>[**IWDFUsbTargetDevice::RetrieveDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)  
デバイスの USB デバイス記述子を取得します。

<a href="" id="iwdfusbtargetdevice--getnuminterfaces"></a>[**IWDFUsbTargetDevice:: GetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)  
デバイスがサポートしている USB インターフェイスの数を取得します。

<a href="" id="iwdfusbtargetdevice--retrieveusbinterface"></a>[**IWDFUsbTargetDevice::RetrieveUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)  
デバイスがサポートするいずれかの USB インターフェイスを公開する[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)インターフェイスへのポインターを取得します。

<a href="" id="iwdfusbtargetdevice--retrievedeviceinformation"></a>[**IWDFUsbTargetDevice::RetrieveDeviceInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedeviceinformation)  
USB デバイスに関連付けられている機能情報を取得します。

<a href="" id="iwdfusbtargetdevice--retrievepowerpolicy"></a>[**IWDFUsbTargetDevice::RetrievePowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievepowerpolicy)  
WinUsb 電源ポリシーを取得します。

<a href="" id="iwdfusbtargetdevice--getwinusbhandle"></a>[**IWDFUsbTargetDevice:: GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getwinusbhandle)  
I/o ターゲットデバイスオブジェクトに関連付けられている WinUsb インターフェイスハンドルを取得します。

### <a href="" id="send-a-control-transfer-to-a-umdf-usb-device-object"></a>UMDF USB デバイスオブジェクトへの制御転送の送信

UMDF ドライバーは、 [**IWDFUsbTargetDevice:: FormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)メソッドを呼び出して、標準、デバイスクラス固有、またはベンダー固有の USB 制御転送を記述する i/o 要求をフォーマットできます。 ドライバーは、 [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出して、同期または非同期で要求を送信できます。

### <a href="" id="set-power-policy-for-a-umdf-usb-device-object"></a>UMDF USB デバイスの電源ポリシーを設定する

UMDF ドライバーは、 [**IWDFUsbTargetDevice:: SetPowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)メソッドを呼び出して、WINUSB が usb デバイス用に使用する電源ポリシーを設定できます。 USB デバイスの電源ポリシーによって、デバイスの電源管理の状態が変わります。

 

 





