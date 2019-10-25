---
title: WDM の情報の取得
description: WDM の情報の取得
ms.assetid: a43ffa5b-6166-4624-8dee-a54aaa8c7283
keywords:
- WDM 情報 WDK KMDF
- 状態情報 WDK KMDF、WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6d60763fd59222e41df36f762624431edfbe74c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844800"
---
# <a name="obtaining-wdm-information"></a>WDM の情報の取得


\[は KMDF にのみ適用され\]

フレームワークには、ドライバーが WDM で定義された情報を取得できるようにするオブジェクトメソッドがいくつか用意されています。

### <a name="obtaining-wdm-information-about-the-driver-and-its-devices"></a>ドライバーとそのデバイスに関する WDM 情報の取得

ドライバーとそのデバイスに関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdffdoinitwdmgetphysicaldevice"></a>[**WdfFdoInitWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitwdmgetphysicaldevice)  
デバイスの物理デバイスオブジェクト (PDO) を表す[**DEVICE_OBJECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造体を取得します。 ドライバーは、デバイスのフレームワークデバイスオブジェクトを作成する前に、このメソッドを呼び出すことができます。

<a href="" id="wdfdevicewdmgetphysicaldevice"></a>[**WdfDeviceWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetphysicaldevice)  
デバイスの PDO を表す WDM デバイス\_オブジェクト構造体を取得します。 ドライバーは、デバイスのフレームワークデバイスオブジェクトを作成した後に、このメソッドを呼び出すことができます。

<a href="" id="wdfdevicewdmgetdeviceobject"></a>[**WdfDeviceWdmGetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetdeviceobject)  
指定されたフレームワークデバイスオブジェクトに関連付けられている WDM デバイスオブジェクトを返します。

<a href="" id="wdfdevicewdmgetattacheddevice"></a>[**WdfDeviceWdmGetAttachedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmgetattacheddevice)  
[デバイススタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)内の次に小さい WDM デバイスオブジェクトを返します。

<a href="" id="wdfwdmdevicegetwdfdevicehandle"></a>[**WdfWdmDeviceGetWdfDeviceHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfwdmdevicegetwdfdevicehandle)  
指定された WDM デバイスオブジェクトに関連付けられているフレームワークデバイスオブジェクトへのハンドルを返します。

<a href="" id="wdfwdmdrivergetwdfdriverhandle"></a>[**WdfWdmDriverGetWdfDriverHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfwdmdrivergetwdfdriverhandle)  
指定された WDM ドライバーオブジェクトに関連付けられているフレームワークドライバーオブジェクトへのハンドルを返します。

### <a name="obtaining-wdm-information-about-io-requests"></a>I/o 要求に関する WDM 情報の取得

I/o 要求に関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdfrequestwdmgetirp"></a>[**WdfRequestWdmGetIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)  
指定されたフレームワーク要求オブジェクトに関連付けられている WDM [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)構造体を返します。 (一方、フレームワーク外で WDM IRP を受信するドライバーは、 [**Wdfrequestcreatefromirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)を呼び出すことによって、irp のフレームワーク要求オブジェクトを作成できます)。

<a href="" id="wdfrequestgetparameters"></a>[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)  
指定されたフレームワーク要求オブジェクトに関連付けられているパラメーターを取得します。 これらのパラメーターのほとんどは、要求の WDM [i/o スタックの場所](https://docs.microsoft.com/windows-hardware/drivers/kernel/i-o-stack-locations)から取得されます)。

<a href="" id="wdfrequestretrieveoutputwdmmdl"></a>[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)  
I/o 要求の出力バッファーを表すメモリ記述子リスト (MDL) を取得します。

<a href="" id="wdfrequestretrieveinputwdmmdl"></a>[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)  
I/o 要求の入力バッファーを表す MDL を取得します。

<a href="" id="wdfrequestformatrequestusingcurrenttype"></a>[**WdfRequestFormatRequestUsingCurrentType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)  
呼び出し元ドライバーの i/o スタックの場所の内容を、ドライバーのローカル i/o ターゲットの i/o スタックの場所にコピーします。

<a href="" id="wdfrequestwdmformatusingstacklocation"></a>[**Stacklocation を指定した wdfrequestwdmformat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation)  
ドライバーのローカル i/o ターゲットの i/o スタックの場所の内容を設定します。

### <a name="obtaining-wdm-information-about-io-targets"></a>I/o ターゲットに関する WDM 情報の取得

I/o ターゲットに関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdfiotargetwdmgettargetdeviceobject"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
ローカルまたはリモートの i/o ターゲットに関連付けられている WDM デバイスオブジェクトへのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfileobject"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
リモート i/o ターゲットに関連付けられている WDM[**ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)構造へのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
リモート i/o ターゲットに関連付けられているファイルへのハンドルを返します。

<a href="" id="wdfiotargetwdmgettargetphysicaldevice"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
リモート i/o ターゲットのデバイスを表す WDM 物理デバイスオブジェクト (PDO) へのポインターを返します。

### <a name="obtaining-wdm-information-about-interrupts-and-dpcs"></a>割り込みと Dpc に関する WDM 情報の取得

割り込みおよび遅延プロシージャ呼び出し (Dpc) に関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdfinterruptwdmgetinterrupt"></a>[**WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)  
指定されたフレームワークの割り込みオブジェクトに関連付けられている WDM [**Kinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体へのポインターを返します。

<a href="" id="wdfdpcwdmgetdpc"></a>[**WdfDpcWdmGetDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcwdmgetdpc)  
指定されたフレームワーク DPC オブジェクトに関連付けられている WDM [**Kdpc**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体へのポインターを返します。

### <a href="" id="obtaining-wdm-information-about-usb-i-o-targets"></a>USB i/o ターゲットに関する WDM 情報の取得

USB i/o ターゲットに関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdfusbtargetpipewdmgetpipehandle"></a>[**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
指定されたフレームワークパイプオブジェクトに関連付けられているハンドル型ハンドル\_USBD\_パイプを返します。

### <a name="obtaining-wdm-information-about-the-registry"></a>レジストリに関する WDM 情報の取得

レジストリに関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdfregistrywdmgethandle"></a>[**WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)  
フレームワークのレジストリキーオブジェクトが表すレジストリキーへの WDM ハンドルを返します。

### <a name="obtaining-wdm-information-about-file-objects"></a>ファイルオブジェクトに関する WDM 情報の取得

ファイルオブジェクトに関する WDM 情報を取得するために、ドライバーは次のメソッドを呼び出すことができます。

<a href="" id="wdffileobjectwdmgetfileobject"></a>[**Wdffileを Twdmgetfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectwdmgetfileobject)  
指定されたフレームワークファイルオブジェクトに関連付けられている、WDM[**ファイル\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)構造体を返します。

 

 





