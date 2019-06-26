---
title: WDM の情報の取得
description: WDM の情報の取得
ms.assetid: a43ffa5b-6166-4624-8dee-a54aaa8c7283
keywords:
- WDM 情報 WDK KMDF
- ステータス情報 WDK KMDF、WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feed9d5423023203bde627bacc8e4baaa5ed9422
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375061"
---
# <a name="obtaining-wdm-information"></a>WDM の情報の取得


\[KMDF にのみ適用されます。\]

フレームワークは、WDM が定義した情報を取得するには、ドライバーを有効にするいくつかのオブジェクトのメソッドを提供します。

### <a name="obtaining-wdm-information-about-the-driver-and-its-devices"></a>WDM 情報は、ドライバーとそのデバイスの取得

WDM については、ドライバーとそのデバイスを取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdffdoinitwdmgetphysicaldevice"></a>[**WdfFdoInitWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitwdmgetphysicaldevice)  
取得、 [ **DEVICE_OBJECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)デバイスの物理デバイス オブジェクト (PDO) を表す構造体です。 ドライバーは、ドライバーがデバイスの framework デバイス オブジェクトを作成する前に、このメソッドを呼び出すことができます。

<a href="" id="wdfdevicewdmgetphysicaldevice"></a>[**WdfDeviceWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetphysicaldevice)  
WDM デバイスを取得\_デバイスの PDO を表すオブジェクトの構造体。 デバイスの framework デバイス オブジェクトが作成した後、ドライバーはこのメソッドを呼び出すことができます。

<a href="" id="wdfdevicewdmgetdeviceobject"></a>[**WdfDeviceWdmGetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject)  
指定のフレームワークのデバイス オブジェクトに関連付けられている WDM デバイス オブジェクトを返します。

<a href="" id="wdfdevicewdmgetattacheddevice"></a>[**WdfDeviceWdmGetAttachedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmgetattacheddevice)  
次の下位 WDM デバイス オブジェクトを返す、[デバイス スタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)します。

<a href="" id="wdfwdmdevicegetwdfdevicehandle"></a>[**WdfWdmDeviceGetWdfDeviceHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfwdmdevicegetwdfdevicehandle)  
指定した WDM デバイス オブジェクトに関連付けられている framework デバイス オブジェクトのハンドルを返します。

<a href="" id="wdfwdmdrivergetwdfdriverhandle"></a>[**WdfWdmDriverGetWdfDriverHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfwdmdrivergetwdfdriverhandle)  
指定した WDM ドライバー オブジェクトに関連付けられている framework ドライバー オブジェクトへのハンドルを返します。

### <a name="obtaining-wdm-information-about-io-requests"></a>WDM I/O 要求情報の取得

WDM I/O 要求情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfrequestwdmgetirp"></a>[**WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)  
返します、WDM [ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)指定のフレームワークの要求オブジェクトに関連付けられている構造体。 (これに対して、ドライバー、フレームワーク外 WDM IRP を受信するオブジェクトを作成できます framework 要求 IRP の呼び出して[ **WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp))。

<a href="" id="wdfrequestgetparameters"></a>[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)  
指定のフレームワークの要求オブジェクトに関連付けられているパラメーターを取得します。 これらのパラメーターのほとんどが、要求の WDM 由来[I/O スタックの場所](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations))。

<a href="" id="wdfrequestretrieveoutputwdmmdl"></a>[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)  
I/O 要求の出力バッファーを表すメモリ記述子一覧 (MDL) を取得します。

<a href="" id="wdfrequestretrieveinputwdmmdl"></a>[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)  
I/O 要求の入力バッファーを表す MDL を取得します。

<a href="" id="wdfrequestformatrequestusingcurrenttype"></a>[**WdfRequestFormatRequestUsingCurrentType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)  
ドライバーのローカルの I/O 対象の I/O スタックの場所には、呼び出し元のドライバーの I/O スタックの場所の内容をコピーします。

<a href="" id="wdfrequestwdmformatusingstacklocation"></a>[**WdfRequestWdmFormatUsingStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation)  
ドライバーのローカルの I/O ターゲットに対して I/O スタックの場所の内容を設定します。

### <a name="obtaining-wdm-information-about-io-targets"></a>WDM I/O ターゲット情報の取得

WDM I/O ターゲット情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfiotargetwdmgettargetdeviceobject"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
ローカルまたはリモートの I/O ターゲットに関連付けられている WDM デバイス オブジェクトへのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfileobject"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
WDM へのポインターを返します[**ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)リモート I/O ターゲットに関連付けられている構造体。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
リモートの I/O ターゲットに関連付けられているファイル ハンドルを返します。

<a href="" id="wdfiotargetwdmgettargetphysicaldevice"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
リモートの I/O ターゲット デバイスを表す WDM 物理デバイス オブジェクト (PDO) へのポインターを返します。

### <a name="obtaining-wdm-information-about-interrupts-and-dpcs"></a>割り込みおよび Dpc をに関する WDM 情報の取得

割り込みと遅延プロシージャ呼び出し (Dpc) に関する WDM 情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfinterruptwdmgetinterrupt"></a>[**WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)  
WDM へのポインターを返します[ **KINTERRUPT** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)指定のフレームワークの割り込みオブジェクトに関連付けられている構造体。

<a href="" id="wdfdpcwdmgetdpc"></a>[**WdfDpcWdmGetDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcwdmgetdpc)  
WDM へのポインターを返します[ **KDPC** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)指定のフレームワークの DPC オブジェクトに関連付けられている構造体。

### <a href="" id="obtaining-wdm-information-about-usb-i-o-targets"></a> WDM USB I/O ターゲット情報の取得

WDM USB I/O ターゲット情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetpipewdmgetpipehandle"></a>[**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
返します、USBD\_パイプ\_指定のフレームワークのパイプ オブジェクトに関連付けられているハンドルに型指定されたハンドル。

### <a name="obtaining-wdm-information-about-the-registry"></a>WDM レジストリ情報の取得

WDM レジストリ情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdfregistrywdmgethandle"></a>[**WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)  
Framework のレジストリ キー オブジェクトが表すレジストリ キーに WDM ハンドルを返します。

### <a name="obtaining-wdm-information-about-file-objects"></a>WDM ファイル オブジェクトの情報を取得します。

WDM ファイル オブジェクトの情報を取得するには、ドライバーは、次のメソッドを呼び出すことができます。

<a href="" id="wdffileobjectwdmgetfileobject"></a>[**WdfFileObjectWdmGetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectwdmgetfileobject)  
WDM 返します[**ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)指定のフレームワークのファイル オブジェクトに関連付けられている構造体。

 

 





