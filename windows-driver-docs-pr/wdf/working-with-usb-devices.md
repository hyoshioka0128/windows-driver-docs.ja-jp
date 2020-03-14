---
title: USB デバイスの使用
description: このトピックでは、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) ドライバーが、Windows ドライバーフレームワーク (WDF) によって提供される USB デバイスオブジェクトメソッドを使用して実行できる操作について説明します。
ms.assetid: 8e06f3c4-1a58-4b9f-ae89-ff4e37eb8f0a
keywords:
- USB i/o ターゲット WDK KMDF、framework USB デバイスオブジェクト
- フレームワークオブジェクト WDK KMDF、USB デバイスオブジェクト
- USB 要求が WDK KMDF をブロックする
- URBs WDK KMDF
- USB i/o ターゲットは、WDK KMDF、USB デバイスです。
- 制御転送 WDK KMDF
- 電源サイクルポート WDK KMDF
- ポート WDK KMDF のリセット
- URBs WDK KMDF の送信
- Unicode 文字列 WDK KMDF
- 状態情報 WDK KMDF、USB i/o ターゲット
- デバイスオブジェクト WDK KMDF
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7b5b5eab473fd32aecae832c702267c6aaa1bafa
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79243023"
---
# <a name="working-with-usb-devices"></a>USB デバイスの使用


このトピックでは、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) ドライバーが、Windows ドライバーフレームワーク (WDF) によって提供される USB デバイスオブジェクトメソッドを使用して実行できる操作について説明します。

このトピックは、次のセクションで構成されています。

-   [USB デバイスオブジェクトの作成](#creating-a-framework-usb-device-object)
-   [USB デバイスの構成](#selecting-a-device-configuration)
-   [デバイス情報の取得](#obtaining-device-information)
-   [USB 記述子の取得](#obtaining-a-device-s-unicode-strings)
-   [制御転送の送信](#sending-a-control-transfer)
-   [デバイスのポートをリセットし、電源を入れ直す](#resetting-and-power-cycling-a-device-s-port)
-   [デバイスへの URB の送信](#sending-a-urb-to-a-device)

単純な KMDF ベースの USB クライアントドライバーを記述する手順の詳細については、「[最初の usb クライアントドライバー (kmdf) を作成する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

## <a href="" id="creating-a-framework-usb-device-object"></a>USB デバイスオブジェクトの作成


フレームワークの USB i/o ターゲットオブジェクト (WDFUSBDEVICE、WDFUSBINTERFACE、WDFUSBPIPE) を使用するには、クライアントドライバーがまず[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出して、usb デバイスオブジェクトを作成する必要があります。 通常、ドライバーは、 [*EvtdeviceWdfUsbTargetDeviceCreateWithParameters ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数から**WdfUsbTargetDeviceCreateWithParameters**を呼び出します。

ドライバーが[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出すと、フレームワークは WDFUSBDEVICE オブジェクトを作成し、USB デバイスを表す FDO に関連付けます。 メソッドは、USB クライアントドライバーが物理デバイスとの通信に使用できる新しいフレームワーク USB デバイスオブジェクトへのハンドルを返します。

[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出した後、ドライバーは[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)および[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)を呼び出して、デバイスから USB 記述子を取得できます。 これらの記述子には、デバイスの最初の構成、そのインターフェイスの設定、定義されているエンドポイントに関する情報が含まれています。 (USB 記述子は、公式の USB 仕様で定義されています)。

## <a href="" id="selecting-a-device-configuration"></a>USB デバイスの構成


また、 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドは、デバイスの最初の構成に含まれる各 usb インターフェイスに対して、フレームワークの usb インターフェイスオブジェクトを作成します。

[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出した後、クライアントドライバーは[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)を呼び出して構成を選択する必要があります。 このメソッドは、選択された構成内のインターフェイスの代替設定ごとに、フレームワークインターフェイスオブジェクトを作成します。

また、このメソッドは、選択した構成の各インターフェイスのそれぞれの代替設定で定義されているエンドポイントを表すパイプオブジェクトを作成します。

構成を選択したら、必要に応じて、構成のインターフェイスの[代替設定を変更](working-with-usb-interfaces.md#selecting-an-alternate-setting-for-a-usb-interface)できます。

[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)を呼び出して、デバイスを deconfigure することもできます。

関連情報については、以下を参照してください。

-   [USB デバイスの構成を選択する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [USB インターフェイスで別の設定を選択する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

## <a href="" id="obtaining-device-information"></a>デバイス情報の取得


デバイスを構成すると、クライアントドライバーは次のメソッドを呼び出して、USB デバイスに関する情報を取得できます。

<a href="" id="wdfusbtargetdevicequeryusbcapability"></a>[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)  
ホストコントローラーと USB ドライバースタックが特定の機能をサポートしているかどうかを判断します。 [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)を呼び出す前に、ドライバーは[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出す必要があります。

<a href="" id="wdfusbtargetdevicegetiotarget"></a>[**WdfUsbTargetDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetiotarget)  
USB デバイスに関連付けられている i/o ターゲットオブジェクトへのハンドルを返します。 ドライバーは、このハンドルを[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)または[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)に渡すことができます。

<a href="" id="wdfusbtargetdeviceretrieveinformation"></a>[**WdfUsbTargetDeviceRetrieveInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveinformation)  
USB デバイスに関連付けられているバージョンと機能の情報を取得します。

<a href="" id="wdfusbtargetdeviceisconnectedsynchronous--kmdf-only-"></a>[**WdfUsbTargetDeviceIsConnectedSynchronous (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceisconnectedsynchronous)  
デバイスが接続されているかどうかを判断します。

<a href="" id="wdfusbtargetdeviceretrievecurrentframenumber--kmdf-only-"></a>[**WdfUsbTargetDeviceRetrieveCurrentFrameNumber (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrievecurrentframenumber)  
現在の USB フレーム番号を取得します。

## <a href="" id="obtaining-a-device-s-unicode-strings"></a>USB 記述子の取得


USB デバイスの記述子に含まれる Unicode 文字列を取得するために、ドライバーは次のいずれかのメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetdevicegetdevicedescriptor"></a>[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)  
デバイスの[USB デバイス記述子](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を取得します。

<a href="" id="wdfusbtargetdeviceretrieveconfigdescriptor"></a>[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)  
デバイスの[USB 構成記述子](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)、インターフェイス記述子、およびエンドポイント記述子を取得します。

<a href="" id="---------wdfusbtargetdevicequerystring--------"></a>[**WdfUsbTargetDeviceQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequerystring)  
Unicode 文字列をドライバーによって指定されたバッファーにコピーします。

<a href="" id="---------wdfusbtargetdeviceallocandquerystring--------"></a>[**WdfUsbTargetDeviceAllocAndQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceallocandquerystring)  
Unicode 文字列をフレームワークによって指定されたバッファーにコピーします。

<a href="" id="---------wdfusbtargetdeviceformatrequestforstring--------"></a>[**WdfUsbTargetDeviceFormatRequestForString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforstring)  
Unicode 文字列の要求を書式設定します。 ドライバーは、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、同期または非同期で要求を送信できます。

## <a href="" id="sending-a-control-transfer"></a>制御転送の送信


ドライバーは、次のメソッドを呼び出して、標準、デバイスクラス固有、またはベンダー固有の USB 制御転送を記述する i/o 要求を送信できます。

<a href="" id="---------wdfusbtargetdevicesendcontroltransfersynchronously--------"></a>[**WdfUsbTargetDeviceSendControlTransferSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)  
USB 制御転送要求を同期的に送信します。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcontroltransfer--------"></a>[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)  
USB 制御転送の要求をフォーマットします。 ドライバーは、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して、同期または非同期で要求を送信できます。

関連情報については、「 [USB 制御転送を送信する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

## <a href="" id="resetting-and-power-cycling-a-device-s-port"></a>デバイスのポートをリセットし、電源を入れ直す


ドライバーは、次のメソッドを呼び出して、デバイスが接続されている USB ポートをリセットまたは電源オフにすることができます。

<a href="" id="---------wdfusbtargetdeviceresetportsynchronously"></a>[**WdfUsbTargetDeviceResetPortSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)  
デバイスの USB ポートをリセットする要求を同期的に送信します。

<a href="" id="---------wdfusbtargetdevicecycleportsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceCyclePortSynchronously (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecycleportsynchronously)  
デバイスの USB ポートの電源をオンにする要求を同期的に送信します。

<a href="" id="---------wdfusbtargetdeviceformatrequestforcycleport--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForCyclePort (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport)  
デバイスの USB ポートの電源をオンにする要求をフォーマットします。 ドライバーは、同期または非同期で要求を送信するために、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出す必要があります。

関連情報については、「 [USB パイプのエラーから回復する方法](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)」を参照してください。

## <a href="" id="sending-a-urb-to-a-device"></a>デバイスへの URB の送信


KMDF ドライバーが URBs を含む i/o 要求を送信して USB デバイスと通信する場合、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetdevicecreateurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateUrb (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)  
USB 要求ブロック (URB) を割り当てます。 [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)を呼び出す前に、ドライバーは[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出す必要があります。

<a href="" id="wdfusbtargetdevicecreateisochurb--kmdf-only-"></a>[**WdfUsbTargetDeviceCreateIsochUrb (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)  
アイソクロナス USB 要求ブロック (URB) を割り当てます。 [**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)を呼び出す前に、ドライバーは[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出す必要があります。

<a href="" id="---------wdfusbtargetdevicesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetDeviceSendUrbSynchronously (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)  
URB を含む i/o 要求を同期的に送信します。

<a href="" id="---------wdfusbtargetdeviceformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetDeviceFormatRequestForUrb (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)  
URB を含む i/o 要求の形式を設定します。 ドライバーは、同期または非同期で要求を送信するために、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出す必要があります。

<a href="" id="---------wdfusbtargetdevicewdmgetconfigurationhandle--kmdf-only-"></a>[**WdfUsbTargetDeviceWdmGetConfigurationHandle (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicewdmgetconfigurationhandle)  
デバイスの USBD 構成ハンドルを返します。 一部の URBs では、このハンドルが必要です。

URBs の一般的な概念の背景については、「 [URBs の割り当てとビルド](https://docs.microsoft.com/windows-hardware/drivers/usbcon/how-to-add-xrb-support-for-client-drivers)」を参照してください。

 

 





