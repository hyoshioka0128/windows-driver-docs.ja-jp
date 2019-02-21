---
title: WDM 情報を取得します。
description: WDM 情報を取得します。
ms.assetid: a43ffa5b-6166-4624-8dee-a54aaa8c7283
keywords:
- WDM 情報 WDK KMDF
- ステータス情報 WDK KMDF、WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93ec3ef372af5867f79e92417d9533967cbcd48d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536920"
---
# <a name="obtaining-wdm-information"></a>WDM 情報を取得します。


\[KMDF にのみ適用されます。\]

フレームワークは、WDM が定義した情報を取得するには、ドライバーを有効にするいくつかのオブジェクトのメソッドを提供します。

### <a name="obtaining-wdm-information-about-the-driver-and-its-devices"></a>WDM 情報は、ドライバーとそのデバイスの取得

WDM については、ドライバーとそのデバイスを取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdffdoinitwdmgetphysicaldevice"></a>[**WdfFdoInitWdmGetPhysicalDevice**](https://msdn.microsoft.com/library/windows/hardware/ff547281)  
取得、 [ **DEVICE_OBJECT** ](https://msdn.microsoft.com/library/windows/hardware/ff543147)デバイスの物理デバイス オブジェクト (PDO) を表す構造体です。 ドライバーは、ドライバーがデバイスの framework デバイス オブジェクトを作成する前に、このメソッドを呼び出すことができます。

<a href="" id="wdfdevicewdmgetphysicaldevice"></a>[**WdfDeviceWdmGetPhysicalDevice**](https://msdn.microsoft.com/library/windows/hardware/ff546946)  
WDM デバイスを取得\_デバイスの PDO を表すオブジェクトの構造体。 デバイスの framework デバイス オブジェクトが作成した後、ドライバーはこのメソッドを呼び出すことができます。

<a href="" id="wdfdevicewdmgetdeviceobject"></a>[**WdfDeviceWdmGetDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff546942)  
指定のフレームワークのデバイス オブジェクトに関連付けられている WDM デバイス オブジェクトを返します。

<a href="" id="wdfdevicewdmgetattacheddevice"></a>[**WdfDeviceWdmGetAttachedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff546934)  
次の下位 WDM デバイス オブジェクトを返す、[デバイス スタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)します。

<a href="" id="wdfwdmdevicegetwdfdevicehandle"></a>[**WdfWdmDeviceGetWdfDeviceHandle**](https://msdn.microsoft.com/library/windows/hardware/ff551175)  
指定した WDM デバイス オブジェクトに関連付けられている framework デバイス オブジェクトのハンドルを返します。

<a href="" id="wdfwdmdrivergetwdfdriverhandle"></a>[**WdfWdmDriverGetWdfDriverHandle**](https://msdn.microsoft.com/library/windows/hardware/ff551176)  
指定した WDM ドライバー オブジェクトに関連付けられている framework ドライバー オブジェクトへのハンドルを返します。

### <a name="obtaining-wdm-information-about-io-requests"></a>WDM I/O 要求情報の取得

WDM I/O 要求情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfrequestwdmgetirp"></a>[**WdfRequestWdmGetIrp**](https://msdn.microsoft.com/library/windows/hardware/ff550037)  
返します、WDM [ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)指定のフレームワークの要求オブジェクトに関連付けられている構造体。 (これに対して、ドライバー、フレームワーク外 WDM IRP を受信するオブジェクトを作成できます framework 要求 IRP の呼び出して[ **WdfRequestCreateFromIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549953))。

<a href="" id="wdfrequestgetparameters"></a>[**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)  
指定のフレームワークの要求オブジェクトに関連付けられているパラメーターを取得します。 これらのパラメーターのほとんどが、要求の WDM 由来[I/O スタックの場所](https://msdn.microsoft.com/library/windows/hardware/ff551821))。

<a href="" id="wdfrequestretrieveoutputwdmmdl"></a>[**WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)  
I/O 要求の出力バッファーを表すメモリ記述子一覧 (MDL) を取得します。

<a href="" id="wdfrequestretrieveinputwdmmdl"></a>[**WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)  
I/O 要求の入力バッファーを表す MDL を取得します。

<a href="" id="wdfrequestformatrequestusingcurrenttype"></a>[**WdfRequestFormatRequestUsingCurrentType**](https://msdn.microsoft.com/library/windows/hardware/ff549955)  
ドライバーのローカルの I/O 対象の I/O スタックの場所には、呼び出し元のドライバーの I/O スタックの場所の内容をコピーします。

<a href="" id="wdfrequestwdmformatusingstacklocation"></a>[**WdfRequestWdmFormatUsingStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550036)  
ドライバーのローカルの I/O ターゲットに対して I/O スタックの場所の内容を設定します。

### <a name="obtaining-wdm-information-about-io-targets"></a>WDM I/O ターゲット情報の取得

WDM I/O ターゲット情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfiotargetwdmgettargetdeviceobject"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff548682)  
ローカルまたはリモートの I/O ターゲットに関連付けられている WDM デバイス オブジェクトへのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfileobject"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548686)  
WDM へのポインターを返します[**ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff545834)リモート I/O ターゲットに関連付けられている構造体。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://msdn.microsoft.com/library/windows/hardware/ff548683)  
リモートの I/O ターゲットに関連付けられているファイル ハンドルを返します。

<a href="" id="wdfiotargetwdmgettargetphysicaldevice"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548691)  
リモートの I/O ターゲット デバイスを表す WDM 物理デバイス オブジェクト (PDO) へのポインターを返します。

### <a name="obtaining-wdm-information-about-interrupts-and-dpcs"></a>割り込みおよび Dpc をに関する WDM 情報の取得

割り込みと遅延プロシージャ呼び出し (Dpc) に関する WDM 情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfinterruptwdmgetinterrupt"></a>[**WdfInterruptWdmGetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff547393)  
WDM へのポインターを返します[ **KINTERRUPT** ](https://msdn.microsoft.com/library/windows/hardware/ff554237)指定のフレームワークの割り込みオブジェクトに関連付けられている構造体。

<a href="" id="wdfdpcwdmgetdpc"></a>[**WdfDpcWdmGetDpc**](https://msdn.microsoft.com/library/windows/hardware/ff547167)  
WDM へのポインターを返します[ **KDPC** ](https://msdn.microsoft.com/library/windows/hardware/ff551882)指定のフレームワークの DPC オブジェクトに関連付けられている構造体。

### <a href="" id="obtaining-wdm-information-about-usb-i-o-targets"></a> WDM USB I/O ターゲット情報の取得

WDM USB I/O ターゲット情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetpipewdmgetpipehandle"></a>[**WdfUsbTargetPipeWdmGetPipeHandle**](https://msdn.microsoft.com/library/windows/hardware/ff551162)  
返します、USBD\_パイプ\_指定のフレームワークのパイプ オブジェクトに関連付けられているハンドルに型指定されたハンドル。

### <a name="obtaining-wdm-information-about-the-registry"></a>WDM レジストリ情報の取得

WDM レジストリ情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfregistrywdmgethandle"></a>[**WdfRegistryWdmGetHandle**](https://msdn.microsoft.com/library/windows/hardware/ff549935)  
Framework のレジストリ キー オブジェクトが表すレジストリ キーに WDM ハンドルを返します。

### <a name="obtaining-wdm-information-about-file-objects"></a>WDM ファイル オブジェクトの情報を取得します。

WDM ファイル オブジェクトの情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdffileobjectwdmgetfileobject"></a>[**WdfFileObjectWdmGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff547324)  
WDM 返します[**ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff545834)指定のフレームワークのファイル オブジェクトに関連付けられている構造体。

 

 





