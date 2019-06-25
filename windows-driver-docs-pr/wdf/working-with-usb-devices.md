---
title: USB デバイスの使用
description: このトピックでは、バージョン 2 以降では、カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) ドライバーを Windows Driver Frameworks (WDF) によって提供されている USB デバイス オブジェクトのメソッドを使用して実行できる操作について説明します。
ms.assetid: 8e06f3c4-1a58-4b9f-ae89-ff4e37eb8f0a
keywords:
- USB I/O ターゲット WDK KMDF、フレームワークの USB デバイス オブジェクト
- フレームワークは、WDK KMDF、USB デバイス オブジェクトをオブジェクトします。
- USB 要求 WDK KMDF をブロックします。
- 翻訳の WDK KMDF
- USB I/O ターゲット WDK KMDF、USB デバイス
- コントロールは、WDK KMDF を転送します。
- ポート WDK KMDF の電源を入れ直す
- WDK KMDF のポートをリセットします。
- 翻訳の WDK KMDF を送信します。
- WDK KMDF の Unicode 文字列します。
- WDK KMDF、USB I/O ターゲットの状態情報
- デバイス オブジェクト WDK KMDF
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: c1b40a726288e78e1d61d10f622f6dcd5eb374c5
ms.sourcegitcommit: b13b4947916a2237af3a00792c0f4f2ef33877c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2019
ms.locfileid: "67346443"
---
# <a name="working-with-usb-devices"></a>USB デバイスの使用


このトピックでは、バージョン 2 以降では、カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) ドライバーを Windows Driver Frameworks (WDF) によって提供されている USB デバイス オブジェクトのメソッドを使用して実行できる操作について説明します。

次のセクションが含まれています。

-   [USB デバイス オブジェクトを作成します。](#creating-a-framework-usb-device-object)
-   [USB デバイスを構成します。](#selecting-a-device-configuration)
-   [デバイス情報を取得します。](#obtaining-device-information)
-   [USB の記述子を取得します。](#obtaining-a-device-s-unicode-strings)
-   [コントロールの転送を送信します。](#sending-a-control-transfer)
-   [リセットして、電源を入れ直すデバイスのポート](#resetting-and-power-cycling-a-device-s-port)
-   [デバイスに、URB を送信します。](#sending-a-urb-to-a-device)

単純な KMDF ベースの USB クライアント ドライバーの記述に関する詳細な手順は、次を参照してください。 [、最初の USB クライアント ドライバー (KMDF) を書き込む方法](https://msdn.microsoft.com/library/windows/hardware/hh706187)します。

## <a href="" id="creating-a-framework-usb-device-object"></a> USB デバイス オブジェクトを作成します。


フレームワークの USB I/O ターゲット オブジェクト (WDFUSBDEVICE、WDFUSBINTERFACE、および WDFUSBPIPE) を使用するには、クライアント ドライバーは呼び出す必要がありますまず[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428) USB デバイスを作成するにはオブジェクト。 通常、ドライバーを呼び出す**WdfUsbTargetDeviceCreateWithParameters**からその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数。

ドライバーを呼び出すと[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)フレームワークが WDFUSBDEVICE オブジェクトを作成し、USB デバイスを表す FDO に関連付けます。 メソッドは、USB クライアント ドライバーは物理デバイスと通信するために使用できる、新しいフレームワーク USB デバイス オブジェクトのハンドルを返します。

呼び出した後[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)、ドライバーが呼び出せる[ **WdfUsbTargetDeviceGetDeviceDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550090)[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)デバイスから USB 記述子を取得します。 これらの記述子では、デバイスの最初の構成、そのインターフェイスの設定、およびそのエンドポイントが定義されてについてを説明します。 (USB 記述子は、公式の USB 仕様で定義されます)。

## <a href="" id="selecting-a-device-configuration"></a>USB デバイスを構成します。


[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)も、メソッドは、デバイスの最初の構成を含む USB インターフェイスごとに framework USB インターフェイス オブジェクトを作成します。

呼び出した後[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)、クライアント ドライバーを呼び出す必要があります[ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101)構成を選択します。 このメソッドは、選択した構成でインターフェイスの代替各設定のフレームワーク インターフェイス オブジェクトを作成します。

メソッドには、選択した構成の各インターフェイスの各代替の設定で定義されたエンドポイントを表すオブジェクトをパイプも作成します。

後に、構成を選択したら、[代替設定を変更する](working-with-usb-interfaces.md#selecting-an-alternate-setting-for-a-usb-interface)構成のインターフェイスでは、必要な場合。

呼び出すこともできます[ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101)デバイスの構成を解除します。

関連情報については、次を参照してください。

-   [USB デバイスの構成を選択する方法](https://msdn.microsoft.com/library/windows/hardware/gg615081)
-   [USB インターフェイスで代替の設定を選択する方法](https://msdn.microsoft.com/library/windows/hardware/hh968309)

## <a href="" id="obtaining-device-information"></a> デバイス情報を取得します。


デバイスを構成した後、クライアント ドライバーは、USB デバイスに関する情報を取得する次のメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetdevicequeryusbcapability"></a>[**WdfUsbTargetDeviceQueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh439434)  
ホスト コント ローラーと USB ドライバー スタックが特定の機能をサポートするかどうかを判断します。 呼び出しの前に[ **WdfUsbTargetDeviceQueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh439434)、ドライバーを呼び出す必要があります[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)します。

<a href="" id="wdfusbtargetdevicegetiotarget"></a>[**WdfUsbTargetDeviceGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff550093)  
USB デバイスに関連付けられている I/O ターゲット オブジェクトにハンドルを返します。 ドライバーはこのハンドルを渡すことができます[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)または[ **WdfIoTargetStop**](https://msdn.microsoft.com/library/windows/hardware/ff548680)します。

<a href="" id="wdfusbtargetdeviceretrieveinformation"></a>[**WdfUsbTargetDeviceRetrieveInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550100)  
USB デバイスに関連付けられているバージョンと機能の情報を取得します。

<a href="" id="wdfusbtargetdeviceisconnectedsynchronous--kmdf-only-"></a>[**WdfUsbTargetDeviceIsConnectedSynchronous (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff550095)  
デバイスが接続されているかどうかを決定します。

<a href="" id="wdfusbtargetdeviceretrievecurrentframenumber--kmdf-only-"></a>[**WdfUsbTargetDeviceRetrieveCurrentFrameNumber (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff550099)  
USB の現在のフレーム数を取得します。

## <a href="" id="obtaining-a-device-s-unicode-strings"></a>USB の記述子を取得します。


USB デバイスの記述子に含まれる Unicode 文字列を取得するには、ドライバーは、次のメソッドのいずれかを呼び出すことができます。

<a href="" id="wdfusbtargetdevicegetdevicedescriptor"></a>[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550090)  
デバイスの取得[USB デバイス記述子](https://msdn.microsoft.com/library/windows/hardware/ff539283)します。

<a href="" id="wdfusbtargetdeviceretrieveconfigdescriptor"></a>[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550098)  
デバイスの取得[USB 構成記述子](https://msdn.microsoft.com/library/windows/hardware/ff539242)インターフェイスの記述子、およびエンドポイント記述子。

<a href="" id="---------wdfusbtargetdevicequerystring--------"></a>[**WdfUsbTargetDeviceQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff550096)  
ドライバーによって提供されるバッファーに Unicode 文字列をコピーします。

<a href="" id="---------wdfusbtargetdeviceallocandquerystring--------"></a>[**WdfUsbTargetDeviceAllocAndQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff550074)  
フレームワークが指定したバッファーに Unicode 文字列をコピーします。

<a href="" id="---------wdfusbtargetdeviceformatrequestforstring--------"></a>[**WdfUsbTargetDeviceFormatRequestForString**](https://msdn.microsoft.com/library/windows/hardware/ff550086)  
Unicode 文字列の要求を書式設定します。 ドライバーが呼び出せる[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

## <a href="" id="sending-a-control-transfer"></a> コントロールの転送を送信します。


ドライバーは、standard、デバイス クラスに固有の説明する I/O 要求を送信する次のメソッドを呼び出すことができます、またはベンダー固有の USB 制御転送します。

<a href="" id="---------wdfusbtargetdevicesendcontroltransfersynchronously--------"></a>[**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550104)  
同期的に、USB 制御転送要求を送信します。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcontroltransfer--------"></a>[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082)  
USB 制御転送要求を書式設定します。 ドライバーが呼び出せる[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

関連情報については、次を参照してください。 [USB 制御転送を送信する方法](https://msdn.microsoft.com/library/windows/hardware/ff539261)します。

## <a href="" id="resetting-and-power-cycling-a-device-s-port"></a> リセットして、電源を入れ直すデバイスのポート


ドライバーは、リセット、または電源に接続しているデバイスを USB ポートを次のメソッドを呼び出すことができます。

<a href="" id="---------wdfusbtargetdeviceresetportsynchronously"></a>[**WdfUsbTargetDeviceResetPortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550097)  
同期的にデバイスの USB ポートにリセットする要求を送信します。

<a href="" id="---------wdfusbtargetdevicecycleportsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceCyclePortSynchronously (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff550080)  
電源サイクル デバイスの USB ポートに要求を同期的に送信します。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcycleport--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForCyclePort (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff550084)  
電源サイクル デバイスの USB ポートに要求を書式設定します。 ドライバーを呼び出す必要があります[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

関連情報については、次を参照してください。 [USB パイプ エラーから回復する方法](https://msdn.microsoft.com/library/windows/hardware/hh968307)します。

## <a href="" id="sending-a-urb-to-a-device"></a> デバイスに、URB を送信します。


KMDF ドライバーは、翻訳が含まれている I/O 要求を送信することによって、USB デバイスと通信、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetdevicecreateurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateUrb (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)  
USB 要求ブロック (URB) を割り当てます。 呼び出しの前に[ **WdfUsbTargetDeviceCreateUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439423)、ドライバーを呼び出す必要があります[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)します。

<a href="" id="wdfusbtargetdevicecreateisochurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateIsochUrb (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/hh439420)  
アイソクロナス USB 要求ブロック (URB) を割り当てます。 呼び出しの前に[ **WdfUsbTargetDeviceCreateIsochUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439420)、ドライバーを呼び出す必要があります[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)します。

<a href="" id="---------wdfusbtargetdevicesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceSendUrbSynchronously (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff550105)  
同期的に、URB を含む I/O 要求を送信します。

<a href="" id="---------wdfusbtargetdeviceformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForUrb (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff550088)  
含む、URB I/O 要求の書式を設定します。 ドライバーを呼び出す必要があります[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)同期または非同期要求を送信します。

<a href="" id="---------wdfusbtargetdevicewdmgetconfigurationhandle--kmdf-only-"></a>[**WdfUsbTargetDeviceWdmGetConfigurationHandle (KMDF のみ)** ](https://msdn.microsoft.com/library/windows/hardware/ff551127)  
デバイスの USBD 構成ハンドルを返します。 いくつかの翻訳では、このハンドルが必要です。

翻訳の一般的な概念の背景を参照してください。[割り当てと構成の翻訳](https://docs.microsoft.com/windows-hardware/drivers/usbcon/how-to-add-xrb-support-for-client-drivers)します。

 

 





