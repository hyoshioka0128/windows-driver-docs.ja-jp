---
title: UMDF 1.x ドライバーで USB デバイスの操作
description: UMDF 1.x ドライバーで USB デバイスの操作
ms.assetid: 144898a2-c4e1-495f-a6ca-72d9f09bda90
keywords:
- UMDF WDK、USB デバイス
- ユーザー モード ドライバー フレームワーク WDK、USB デバイス
- ユーザー モード ドライバー WDK UMDF、USB デバイス
- WDK UMDF の USB デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 442e9331715f50289a2bbcc2676964155da68ae7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536807"
---
# <a name="working-with-usb-devices-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーで USB デバイスの操作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、フレームワークの USB デバイス オブジェクトとして各 USB デバイスを表します。 UMDF ドライバーは、ドライバーが USB I/O ターゲット フレームワークのサポートにアクセスできる前に、フレームワークの USB デバイス オブジェクトを作成する必要があります。 UMDF は、UMDF ドライバーを有効にする USB デバイス オブジェクトのメソッドを提供します。

-   [UMDF USB デバイス オブジェクトを作成します。](#creating-a-umdf-usb-device-object)

-   [デバイス情報を取得します。](#obtaining-umdf-usb-device-information)

-   [コントロールの転送を送信します。](#send-a-control-transfer-to-a-umdf-usb-device-object)

-   [電源ポリシーの設定](#set-power-policy-for-a-umdf-usb-device-object)

### <a name="creating-a-umdf-usb-device-object"></a>UMDF USB デバイス オブジェクトを作成します。

フレームワークの USB I/O ターゲット機能を使用する UMDF ドライバーを入手へのポインター、 [IWDFUsbTargetFactory](https://msdn.microsoft.com/library/windows/hardware/ff560387)インターフェイス。 ポインターを取得するには、ドライバーを呼び出す必要があります、 **QueryInterface**メソッド、デバイスの[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)インターフェイス。 次のコード例は、呼び出す方法を示しています。 **QueryInterface**ポインターを取得します。

```cpp
hr = pdevice->QueryInterface(IID_IWDFUsbTargetFactory, (LPVOID*)&ppUsbTargetFactory);
```

ドライバーが次に呼び出す必要があります、 [ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560390)デバイスの USB I/O ターゲット オブジェクトを作成します。 ドライバーが USB I/O ターゲットを作成した後、ドライバーは、I/O ターゲットに要求を送信できます。 通常、ドライバー呼び出し**IWDFUsbTargetFactory::CreateUsbTargetDevice**内から、 [ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)コールバック関数。

ドライバーの呼び出し後**IWDFUsbTargetFactory::CreateUsbTargetDevice**、ドライバーは[USB デバイスの情報を取得](https://msdn.microsoft.com/library/windows/hardware/ff561472#obtaining-umdf-usb-device-information)(たとえば、USB ディスクリプター デバイス、USB インターフェイス、およびインターフェイスエンドポイントの場合)。 USB 記述子は、USB 仕様で説明します。

### <a name="obtaining-umdf-usb-device-information"></a>UMDF USB デバイスの情報を取得します。

UMDF ドライバーを呼び出してから、 [ **IWDFUsbTargetFactory::CreateUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560390) UMDF USB ターゲット デバイスを作成するメソッドがオブジェクト、ドライバーは、USB デバイスを対象とする、次のメソッドを呼び出すことができますUSB デバイスに関する情報を取得するためにオブジェクトを定義します。

<a href="" id="iwdfusbtargetdevice--retrievedescriptor"></a>[**IWDFUsbTargetDevice::RetrieveDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff560374)  
デバイスの USB デバイスの記述子を取得します。

<a href="" id="iwdfusbtargetdevice--getnuminterfaces"></a>[**IWDFUsbTargetDevice::GetNumInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff560366)  
デバイスをサポートする USB インターフェイスの数を取得します。

<a href="" id="iwdfusbtargetdevice--retrieveusbinterface"></a>[**IWDFUsbTargetDevice::RetrieveUsbInterface**](https://msdn.microsoft.com/library/windows/hardware/ff560381)  
ポインターを取得、 [IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)いずれかのデバイスをサポートする USB インターフェイスを公開するインターフェイス。

<a href="" id="iwdfusbtargetdevice--retrievedeviceinformation"></a>[**IWDFUsbTargetDevice::RetrieveDeviceInformation**](https://msdn.microsoft.com/library/windows/hardware/ff560377)  
USB デバイスに関連付けられている機能の情報を取得します。

<a href="" id="iwdfusbtargetdevice--retrievepowerpolicy"></a>[**IWDFUsbTargetDevice::RetrievePowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff560379)  
WinUsb 電源ポリシーを取得します。

<a href="" id="iwdfusbtargetdevice--getwinusbhandle"></a>[**IWDFUsbTargetDevice::GetWinUsbHandle**](https://msdn.microsoft.com/library/windows/hardware/ff560369)  
I/O のターゲット デバイス オブジェクトに関連付けられている WinUsb インターフェイスのハンドルを取得します。

### <a href="" id="send-a-control-transfer-to-a-umdf-usb-device-object"></a>UMDF USB デバイス オブジェクトをコントロールの転送を送信します。

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbTargetDevice::FormatRequestForControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff560363) standard では、デバイスにクラスに固有の説明する I/O 要求の書式を指定するメソッドまたはベンダー固有の USBコントロールの転送。 ドライバーを呼び出して、 [ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)同期または非同期要求を送信するメソッド。

### <a href="" id="set-power-policy-for-a-umdf-usb-device-object"></a>UMDF USB デバイスの電源ポリシーの設定

UMDF ドライバーを呼び出すことができます、 [ **IWDFUsbTargetDevice::SetPowerPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff560385) USB デバイス WinUsb によって使用される電源ポリシーを設定します。 USB デバイスの電源ポリシー効果の変更、デバイスの電源管理の状態にします。

 

 





