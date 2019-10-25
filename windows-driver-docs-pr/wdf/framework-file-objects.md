---
title: フレームワーク ファイル オブジェクト
description: フレームワーク ファイル オブジェクト
ms.assetid: 93ec5dd7-8ef0-4cea-9253-ea5d7869d4b8
keywords:
- I/o 要求 WDK KMDF、ファイルオブジェクト
- ファイルオブジェクト WDK KMDF
- WDK KMDF、ファイルオブジェクトを処理する要求
- フレームワークオブジェクト WDK KMDF、ファイルオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e7946f9ddb7a2342aca791c6b7b8ea151b6b827
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843173"
---
# <a name="framework-file-objects"></a>フレームワーク ファイル オブジェクト





アプリケーションまたはドライバーが、通常はファイルを作成または開くことによってデバイスにアクセスしようとすると、オペレーティングシステムからドライバースタックにファイル作成要求が送信されます。 アプリケーションまたはドライバーがデバイスの使用を終了すると、システムは、ファイルのクリーンアップと終了要求をドライバースタックに送信します。 これら3つの要求の[要求の種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_type)は、それぞれ**WdfRequestTypeCreate**、 **WdfRequestTypeCleanup**、および**WdfRequestTypeClose**です。

通常、ドライバーが[**Wdfdeviceinitsetexclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)を呼び出していない場合、ドライバーは、複数のファイルを開くことができるため、ファイルの作成、クリーンアップ、および終了要求を受信するときに、ファイル固有またはその他のアクセス固有の操作を実行する必要があります。同時に、または複数のアプリケーションが同時にデバイスにアクセスできます。 したがって、ドライバーは、各ファイルまたはアプリケーションに関連付けられている i/o 要求を追跡する必要があります。

フレームワークは、ファイル、ディレクトリ、ボリューム、メールスロット、名前付きパイプ、デバイス全体など、デバイスにアクセスするためのアプリケーションまたはドライバーの手段を表す*フレームワークファイルオブジェクト*を定義します。 ファイル名はファイルオブジェクトに関連付けることができますが、ファイル名の意味はドライバーによって異なります。 ファイル名の詳細については、「[デバイスの名前空間へのアクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)」を参照してください。

ドライバーでファイル操作を処理する必要がある場合は、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数内から[**Wdfdeviceinitsetfileobjectconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)を呼び出す必要があります。 **Wdfdeviceinitsetfileobjectconfig**メソッドは、 [**WDF\_FILEOBJECT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)構造体を入力として受け取ります。 ドライバーは、この構造体を使用して[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)、 [*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)、および[*evtfileclose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)コールバック関数を登録し、必要に応じて、次の操作を行うたびにフレームワークがフレームワークファイルオブジェクトを作成する必要があるかどうかを示します。ドライバーは、ファイル作成要求を受信します。

ファイル操作を処理するほとんどのドライバーは、フレームワークファイルオブジェクトの[コンテキスト空間](framework-object-context-space.md)にファイル固有の情報を格納します。 ドライバーがファイルの操作を処理するが、ファイルオブジェクトのコンテキスト空間に情報を格納する必要がない場合、フレームワークはドライバー用のフレームワークファイルオブジェクトを作成する必要はありません。

### <a name="creating-or-opening-a-file"></a>ファイルの作成または開く

フレームワークが関数ドライバーのファイル作成要求を受信すると、次のようになります。

1.  以前にフレームワークファイルオブジェクトを使用する必要がないことをドライバーが指定していない限り、ファイルを表すフレームワークファイルオブジェクトを作成します。

2.  ドライバーがコールバック関数を登録している場合は、ドライバーの[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) callback 関数を呼び出します。

[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) callback 関数は、通常、ファイル名やファイルオブジェクトフラグなど、ファイルに関する[情報を取得](#obtaining-file-information)します。 通常、この情報は、フレームワークファイルオブジェクトのコンテキスト空間に格納されます。

[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数を提供する代わりに、ドライバーは[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出して、すべてのファイル作成要求 (**WdfRequestTypeCreate**要求の種類) を受信するように i/o キューを設定できます。 その後、ドライバーは、キューの[*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)要求ハンドラーでファイル作成要求を受信します。 (キューの[**WDF\_IO\_queue\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体の**Defaultqueue**メンバーが**TRUE**に設定されている場合、i/o キューはファイル作成要求を受信できません)。

ドライバーが[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数を提供しておらず、 **WdfRequestTypeCreate**で型指定された i/o 要求を処理するための i/o キューを設定していない場合、フレームワークは次のようになります。

-   ドライバーが関数ドライバーである場合、\_状態が [成功] になっているドライバーのすべてのファイル作成要求を完了します。

-   ドライバーがフィルタードライバーである場合、すべてのファイル作成要求を次の下位のドライバーに転送します。

(この動作を変更する方法については、 [**WDF\_FILEOBJECT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)構造体の**Autoforwardcleanupclose**メンバーを参照してください)。

**注**   アプリケーションがドライバーのデバイスにアクセスするために使用できる[デバイスインターフェイス](using-device-interfaces.md)が関数ドライバーによって提供されていない場合、ドライバーは、すべてのファイルを完了する[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数を提供する必要があります。NT\_SUCCESS (*状態*) が**FALSE**と等しい状態値を持つ作成要求。 そうしないと、悪意のあるアプリケーションが、デバイスの物理デバイスオブジェクト (PDO) の名前を使用してデバイスにアクセスしようとする可能性があります。 (すべての PDOs に[名前](controlling-device-access-in-kmdf-drivers.md#naming-device-objects-only-when-necessary)が付いています)。

 

ドライバーが作成要求を i/o ターゲットに[転送](forwarding-i-o-requests.md)する場合、ドライバーは、i/o ターゲットからエラー状態の値を受信しない限り、エラー状態の値を指定して要求を[完了](completing-i-o-requests.md)することはできません。 それ以外の場合、下位のドライバーには作成要求が失敗したことが通知されず、ファイルが開いているかのように操作が試行される可能性があります。

ドライバーが作成要求を i/o ターゲットに転送する場合、ドライバーは、 [**WDF\_要求\_送信\_\_\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)を設定できません。そのためには、フレームワークによってのフレームワークファイルオブジェクトが作成されます。作成要求。 このため、ドライバーは、 [**WdfFileObjectNotRequired**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_fileobject_class)フラグも設定しない限り、作成要求に対して\_送信\_と\_忘れるフラグ送信\_オプションを送信するように、WDF\_\_要求を設定することはできません。

ドライバーがエラー状態の作成要求を完了した場合、フレームワークは、フレームワークファイルオブジェクトを削除しますが、ドライバーの[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)または[*evtfileclose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)コールバック関数を呼び出しません。 したがって、ドライバーがファイルオブジェクトのコンテキスト空間の外部にオブジェクト固有の追加メモリを割り当てる場合は、割り当てられたメモリを削除する[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)または[*evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバック関数を指定する必要があります。

Windows Vista 以降では、ファイル作成要求を[取り消す](canceling-i-o-requests.md)ことができます。 以前のバージョンの Windows オペレーティングシステムでは、ファイル作成要求の取り消しはサポートされていません。

システムは、ユーザーアプリケーションからの作成要求ごとに、常に Windows Driver Model (WDM) ファイルオブジェクトを作成します。 ドライバーが作成要求を送信した場合、その要求に対して WDM ファイルオブジェクトが作成されない可能性があります。 通常、WDM ファイルオブジェクトが存在しない場合、フレームワークはフレームワークファイルオブジェクトを作成しません。 ただし、ドライバーが[**Wdfdeviceinitsetexclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)を呼び出し、ドライバーが[**WDF\_FILEOBJECT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)構造体の**Fileobjectclass**メンバーに set [**WdfFileObjectWdfCannotUseFsContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_fileobject_class)を設定している場合は、フレームワークは、WDM ファイルオブジェクトが存在しない場合でも、フレームワークファイルオブジェクトを作成します。

### <a href="" id="obtaining-file-information"></a>ファイル情報の取得

ドライバーの[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) callback 関数は、次のオブジェクトメソッドの1つ以上を呼び出して、デバイスへのアプリケーションまたはドライバーのアクセスに関する情報を取得できます。

<a href="" id="---------wdffileobjectgetfilename--------"></a>[**WdfFileObjectGetFileName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename)  
フレームワークファイルオブジェクトに格納されているファイル名を返します。

<a href="" id="---------wdffileobjectgetflags--------"></a>[**WdfFileObjectGetFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetflags)  
フレームワークファイルオブジェクト内に含まれるフラグを返します。

<a href="" id="---------wdffileobjectwdmgetfileobject--------"></a>[**Wdffileを Twdmgetfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectwdmgetfileobject)  
フレームワークファイルオブジェクトに関連付けられている WDM ファイルオブジェクトを返します。

<a href="" id="---------wdfrequestgetparameters--------"></a>[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)  
フレームワークの要求オブジェクトに関連付けられているパラメーターを取得します。 要求の[種類](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_type)が**WdfRequestTypeCreate**の場合、 [**WDF\_request\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_parameters)構造体の Create member には、ファイル作成要求に関する情報が含まれています **。**

通常、ドライバーはフレームワークファイルオブジェクトのコンテキスト空間にファイル情報を格納します。 ドライバーが i/o キューから i/o 要求を取得すると、ドライバーは[**Wdfrequestgetfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)を呼び出して、要求に関連付けられているフレームワークファイルオブジェクトへのハンドルを取得できます。 ドライバーは、フレームワークファイルオブジェクトのコンテキスト空間に格納されているファイル情報を取得できます。

ドライバーは、 [**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)を呼び出して、特定のファイルに関連付けられている要求の i/o キューを検索できます。

ドライバーが WDM[**デバイス\_のオブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造を指すポインターを持っている場合、ドライバーは[**Wdfdevicegetfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetfileobject)を呼び出して、wdm デバイスオブジェクトに関連付けられているフレームワークファイルオブジェクトへのハンドルを取得できます。

### <a name="closing-a-file"></a>ファイルを閉じる

アプリケーションまたはその他のドライバーがファイルを閉じると、フレームワークはクリーンアップ要求を受け取り、ドライバーに対して close 要求を受け取ります。 フレームワーク:

1.  ドライバーがこれらのコールバック関数を登録している場合は、ドライバーの[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)コールバック関数と[*evtfileclose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)コールバック関数を呼び出します。

2.  ファイルを表すフレームワークファイルオブジェクトを削除します。

ドライバーの[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)および[*evtfileclose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)コールバック関数は、フレームワークファイルオブジェクトへのハンドルを受け取ります。 このドライバーは、 [**Wdffileobjectgetdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetdevice)を呼び出して、フレームワークファイルオブジェクトに関連付けられているフレームワークデバイスオブジェクトを判別できます。

 

 





