---
Description: このトピックでは、静的ストリームの機能について説明します。また、usb クライアントドライバーが USB 3.0 デバイスの一括エンドポイントでストリームを開いたり閉じたりする方法について説明します。
title: USB バルク エンドポイントにおける静的ストリームのオープン/クローズ方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0797008cf70cafb5a82485cad8be7f81ce0a9b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844391"
---
# <a name="how-to-open-and-close-static-streams-in-a-usb-bulk-endpoint"></a>USB バルク エンドポイントにおける静的ストリームのオープン/クローズ方法


このトピックでは、*静的ストリームの機能*について説明します。また、usb クライアントドライバーが usb 3.0 デバイスの一括エンドポイントでストリームを開いたり閉じたりする方法について説明します。

USB 2.0 以前のデバイスでは、一括エンドポイントはエンドポイントを介して1つのデータストリームを送受信できます。 USB 3.0 デバイスでは、一括エンドポイントは、エンドポイントを介して複数のデータストリームを送受信する機能を備えています。

Windows 8 の Microsoft 提供の USB ドライバースタックでは、複数のストリームがサポートされています。 これにより、クライアントドライバーは、USB 3.0 デバイスの一括エンドポイントに関連付けられている各ストリームに、独立した i/o 要求を送信できます。 異なるストリームへの要求はシリアル化されません。

クライアントドライバーの場合、ストリームは同じ特性のセットを持つ複数の論理エンドポイントを表します。 特定のストリームに要求を送信するには、クライアントドライバーがそのストリームへのハンドルを必要とします (エンドポイントのパイプハンドルに似ています)。 ストリームへの i/o 要求の URB は、一括エンドポイントへの i/o 要求の URB に似ています。 唯一の違いは、パイプハンドルです。 I/o 要求をストリームに送信するために、ドライバーはストリームへのパイプハンドルを指定します。

デバイスの構成中に、クライアントドライバーは、選択した構成要求と、必要に応じて選択インターフェイス要求を送信します。 これらの要求は、インターフェイスのアクティブな設定で定義されているエンドポイントにパイプハンドルのセットを取得します。 ストリームをサポートするエンドポイントの場合、エンドポイントパイプハンドルを使用して、ドライバーがストリームを開くまで (次に説明します)、*既定のストリーム*(最初のストリーム) に i/o 要求を送信できます。

クライアントドライバーが既定のストリーム以外のストリームに要求を送信する場合、ドライバーはを開いて、すべてのストリームのハンドルを取得する必要があります。 これを行うために、クライアントドライバーは開くストリームの数を指定することによって、*オープンストリームの要求*を送信します。 クライアントドライバーでストリームの使用が終了した後は、必要に応じて、*終了ストリームの要求*を送信してドライバーを閉じることができます。

カーネルモードドライバーフレームワーク (KMDF) は、静的ストリームを本質的にサポートしていません。 クライアントドライバーは、ストリームを開いたり閉じたりする Windows Driver Model (WDM) スタイルの URBs を送信する必要があります。 このトピックでは、これらの URBs を書式設定して送信する方法について説明します。 ユーザーモードドライバーフレームワーク (UMDF)-クライアントドライバーは、静的ストリーム機能を使用できません。

このトピックには、 **WDM ドライバー**としてラベル付けされているいくつかのメモが含まれています。 ここでは、ストリーム要求を送信する WDM ベースの USB クライアントドライバーのルーチンについて説明します。

### <a name="prerequisites"></a>前提条件

クライアントドライバーでストリームを開いたり閉じたりするには、ドライバーに次のものが必要です。

- [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出しました。

  メソッドを使用するには、クライアントコントラクトバージョンを\_クライアント\_コントラクト\_バージョン\_602 にする必要があります。 このバージョンを指定することにより、クライアントドライバーは一連の規則に従う必要があります。 詳細については、「[ベストプラクティス: URBs の使用](usb-client-driver-contract-in-windows-8.md)」を参照してください。

  この呼び出しは、フレームワークの USB ターゲットデバイスオブジェクトへの WDFUSBDEVICE ハンドルを取得します。 このハンドルは、開いているストリームへの後続の呼び出しを行うために必要です。 通常、クライアントドライバーは、ドライバーの[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベントコールバックルーチンにそれ自体を登録します。

  <strong>WDM ドライバー: * * [ </strong>USBD\_createhandle * *](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)ルーチンを呼び出し、ドライバーの登録に使用する USBD ハンドルを USB ドライバースタックに取得します。

- デバイスを構成し、ストリームをサポートする一括エンドポイントへの WDFUSBPIPE パイプハンドルを取得しました。 パイプハンドルを取得するには、選択した構成のインターフェイスの現在の代替設定で[**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)メソッドを呼び出します。

  \* * WDM ドライバー: * * 選択構成または選択インターフェイスの要求を送信して、USBD パイプハンドルを取得します。 詳細については、「 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。

<a name="instructions"></a>手順
------------

### <a name="how-to-open-static-streams"></a>静的ストリームを開く方法

<a href="" id="open-streams"></a>
1. [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)メソッドを呼び出して、基になる USB ドライバースタックとホストコントローラーが静的ストリーム機能をサポートしているかどうかを確認します。 通常、クライアントドライバーは、ドライバーの[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベントコールバックルーチンでルーチンを呼び出します。

   <strong>WDM ドライバー: * * USBD\_[ </strong>queryusbcapability<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406230>)ルーチンを呼び出します。通常、ドライバーは、ドライバーの開始デバイスルーチンで使用する機能 ([</strong>IRP\_によって、\_デバイス<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff551749>)を起動\_) を照会します。コード例については、「* * USBD\_QueryUsbCapability」を参照してください</strong>。

   次の情報を指定します。

   - クライアントドライバーの登録のために、以前に[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)を呼び出したときに取得された USB デバイスオブジェクトへのハンドル。

     <strong>WDM ドライバー: * * [ </strong>USBD\_createhandle * * の前の呼び出しで取得した USBD ハンドルを渡し](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)ます。

     クライアントドライバーで特定の機能を使用する場合は、ドライバースタックとホストコントローラーが機能をサポートしているかどうかを判断するために、まず基礎となる USB ドライバースタックに対してクエリを実行する必要があります。 機能がサポートされている場合にのみ、ドライバーは機能を使用するための要求を送信する必要があります。 一部の要求には、ストリーム機能 (手順 5. で説明) などの URBs が必要です。 これらの要求については、同じハンドルを使用してクエリ機能を実行し、URBs を割り当てるようにしてください。 これは、ドライバースタックがハンドルを使用して、ドライバーが使用できるサポートされている機能を追跡するためです。

     たとえば、( [**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)を呼び出すことによって) USBD\_ハンドルを取得した場合は、 [**USBD\_queryusbcapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))を呼び出してドライバースタックにクエリを実行し、 [**USBD\_URタック検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)を呼び出して URB を割り当てます。 両方の呼び出しに同じ USBD\_ハンドルを渡します。

     KMDF メソッド[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)と[**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)を呼び出す場合は、これらのメソッド呼び出しで、フレームワークターゲットオブジェクトに対して同じ WDFUSBDEVICE ハンドルを指定します。

   - GUID\_USB\_機能\_静的\_ストリームに割り当てられています。
   - 出力バッファー (USHORT へのポインター)。 完了時には、ホストコントローラーでサポートされているストリームの最大数 (エンドポイントあたり) がバッファーに格納されます。
   - 出力バッファーの長さ (バイト単位)。 ストリームの場合、長さは `sizeof (USHORT)`ます。

2. 返された NTSTATUS 値を評価します。 ルーチンが正常に完了した場合は、状態\_SUCCESS が返されます。静的ストリーム機能はサポートされています。 それ以外の場合、メソッドは適切なエラーコードを返します。
3. 開くストリームの数を決定します。 開くことのできるストリームの最大数は、次の方法で制限されます。
   -   ホストコントローラーでサポートされているストリームの最大数。 この番号は、呼び出し元が指定した出力バッファーで、 [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) (WDM ドライバーの場合は[**USBD\_queryusbcapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))) によって受信されます。 Microsoft 提供の USB ドライバースタックでは、最大255のストリームがサポートされています。 **WdfUsbTargetDeviceQueryUsbCapability**は、ストリームの数を計算する際に、その制限を考慮します。 メソッドは、255より大きい値を返すことはありません。
   -   デバイスのエンドポイントでサポートされるストリームの最大数。 この数値を取得するには、エンドポイントコンパニオン記述子を調べます (「 [**USB\_SUPERSPEED\_エンドポイント\_コンパニオンの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)」を参照してください)。 エンドポイントコンパニオン記述子を取得するには、構成記述子を解析する必要があります。 構成記述子を取得するには、クライアントドライバーで[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)メソッドを呼び出す必要があります。 ヘルパールーチン、 [**USBD\_ParseConfigurationDescriptorEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)と[**USBD\_parsedescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parsedescriptors)を使用する必要があります。 コード例については、「 [How to ENUMERATE USB パイプ](how-to-get-usb-pipe-handles.md)」で RetrieveStreamInfoFromEndpointDesc という名前の関数の例を参照してください。

   ストリームの最大数を特定するには、ホストコントローラーとエンドポイントでサポートされている2つの値のうち、小さい方を選択します。
4. *N 個*の要素を含む[**USBD\_STREAM の配列\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_stream_information)構造体を割り当てます。ここで、 *n*は開くストリームの数です。 クライアントドライバーは、ストリームを使用してドライバーが終了した後に、この配列を解放します。
5. [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッドを呼び出して、オープンストリーム要求の URB を割り当てます。 呼び出しが正常に完了した場合、メソッドは、WDF memory オブジェクトと、USB ドライバースタックによって割り当てられた[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体のアドレスを取得します。

   <strong>WDM ドライバー: * *\_USBD [</strong>を呼び出す * * ルーチンを呼び出し](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)ます。

6. オープンストリーム要求の URB をフォーマットします。 URB では[ **\_urb\_使用して\_静的\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_open_static_streams)構造を開いて要求を定義します。 必要な URB をフォーマットするには、次のようにします。
   -   エンドポイントへの USBD パイプハンドル。 WDF pipe オブジェクトがある場合は、 [**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)メソッドを呼び出して USBD パイプハンドルを取得できます。
   -   ストリーム配列 (手順4で作成)
   -   [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体へのポインター (手順 5. で作成)。

   URB をフォーマットするには、 [**UsbBuildOpenStaticStreamsRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildopenstaticstreamsrequest)を呼び出して、必要な情報をパラメーター値として渡します。 **UsbBuildOpenStaticStreamsRequest**に指定されたストリームの数が、サポートされているストリームの最大数を超えていないことを確認してください。
7. [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出して、URB を WDF request オブジェクトとして送信します。 要求を同期的に送信するには、代わりに[**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)メソッドを呼び出します。

   \* * WDM ドライバー: * * URB を IRP に関連付けて、IRP を USB ドライバースタックに送信します。 詳細については、「 [URB を送信する方法](send-requests-to-the-usb-driver-stack.md)」を参照してください。

8. 要求が完了したら、要求の状態を確認します。

   USB ドライバースタックが要求に失敗した場合、URB ステータスには関連するエラーコードが含まれます。 いくつかの一般的なエラー条件については、「解説」を参照してください。

要求の状態 (IRP または WDF request オブジェクト) が USBD\_STATUS\_SUCCESS を示している場合、要求は正常に完了しています。 完了時に受信した[**USBD\_ストリームの配列\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_stream_information)構造を検査します。 配列には、要求されたストリームに関する情報が格納されます。 USB ドライバースタックは、ハンドル (USBD として受信された\_パイプ\_ハンドル)、ストリーム識別子、最大転送サイズなどのストリーム情報を配列の各構造に設定します。 ストリームは、データを転送するために開かれました。

オープンストリーム要求の場合は、URB と配列を割り当てる必要があります。 クライアントドライバーは、open streams 要求が完了した後に、関連付けられた WDF memory オブジェクトで[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)メソッドを呼び出すことによって、URB を解放する必要があります。 ドライバーが[**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)を呼び出して要求を同期的に送信した場合、メソッドから制御が戻った後、WDF memory オブジェクトを解放する必要があります。 クライアントドライバーが[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出すことによって要求を非同期に送信した場合、ドライバーは、要求に関連付けられているドライバーによって実装された完了ルーチンで WDF memory オブジェクトを解放する必要があります。

ストリーム配列は、クライアントドライバーがストリームを使用して終了した後、または i/o 要求用に格納した後に解放できます。 このトピックに記載されているコード例では、ドライバーはストリーム配列をデバイスコンテキストに格納します。 デバイスオブジェクトが削除される直前に、ドライバーによってデバイスコンテキストが解放されます。

### <a name="how-to-transfer-data-to-a-particular-stream"></a>特定のストリームにデータを転送する方法

データ転送要求を特定のストリームに送信するには、WDF request オブジェクトが必要です。 通常、クライアントドライバーは、WDF request オブジェクトを割り当てる必要はありません。 I/o マネージャーは、アプリケーションから要求を受信すると、要求に対して IRP を作成します。 この IRP は、フレームワークによってインターセプトされます。 次に、フレームワークは、IRP を表す WDF request オブジェクトを割り当てます。 その後、フレームワークは WDF request オブジェクトをクライアントドライバーに渡します。 その後、クライアントドライバーは、要求オブジェクトをデータ転送の URB に関連付けて、USB ドライバースタックに送信することができます。

クライアントドライバーがフレームワークから WDF request オブジェクトを受信せず、要求を非同期に送信する場合、ドライバーは[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)メソッドを呼び出すことによって WDF request オブジェクトを割り当てる必要があります。 [**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)を呼び出して新しいオブジェクトを書式設定し、 [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して要求を送信します。

同期の場合、WDF request オブジェクトの引き渡しは任意です。

ストリームにデータを転送するには、URBs を使用する必要があります。 [**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)を呼び出すことによって、URB をフォーマットする必要があります。

次の WDF メソッドは、ストリームではサポートされて*いません*。

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)
-   [**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

次の手順では、クライアントドライバーがフレームワークから要求オブジェクトを受け取ることを前提としています。

1.  [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)を呼び出して URB を割り当てます。 このメソッドは、新しく割り当てられた URB を含む WDF memory オブジェクトを割り当てます。 クライアントドライバーは、すべての i/o 要求に対して URB を割り当てるか、または URB を割り当てて同じ種類の要求に再利用するかを選択できます。
2.  [**UsbBuildInterruptOrBulkTransferRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildinterruptorbulktransferrequest)を呼び出して、一括転送の URB をフォーマットします。 *PipeHandle*パラメーターで、ストリームへのハンドルを指定します。 ストリームハンドルは、前の要求で取得されました。詳細については、「[静的ストリームを開く方法](#open-streams)」を参照してください。
3.  [**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)メソッドを呼び出して、WDF request オブジェクトの書式を設定します。 呼び出しで、データ転送の URB を含む WDF memory オブジェクトを指定します。 メモリオブジェクトが手順 1. で割り当てられました。
4.  [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)または[**WdfUsbTargetPipeSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipesendurbsynchronously)を呼び出すことによって、URB を WDF 要求として送信します。 **Wdfrequestsend**を呼び出す場合、クライアントドライバーが非同期操作の完了時に通知を受け取ることができるように、 [**Wdfrequestsetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)を呼び出して完了ルーチンを指定する必要があります。 完了ルーチンでデータ転送の URB を解放する必要があります。

<strong>WDM ドライバー: * *\_USBD [</strong>を呼び出して urb を割り当て、一括<strong>](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)転送用にフォーマットします (\_[</strong> URB\_BULK\_または\_INTERRUPT\_transfer<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff540352>)) を参照してください。URB をフォーマットするには、UsbBuildInterruptOrBulkTransferRequest [ </strong><strong> ](<https://msdn.microsoft.com/library/windows/hardware/ff538953>)を呼び出すか、または手動で urb 構造をフォーマットします。URB の * * UrbBulkOrInterruptTransfer メンバーでストリームへのハンドルを指定</strong>します。

### <a name="how-to-close-static-streams"></a>静的ストリームを閉じる方法

クライアントドライバーは、ドライバーの使用が終了した後で、ストリームを閉じることができます。 ただし、ストリームの終了要求は省略可能です。 ストリームに関連付けられているエンドポイントが構成解除されると、USB ドライバースタックはすべてのストリームを閉じます。 エンドポイントは、代替の構成またはインターフェイスが選択されている場合、デバイスが削除された場合などに、構成が解除されます。 ドライバーが異なる数のストリームを開こうとする場合は、クライアントドライバーでストリームを閉じる必要があります。 ストリームの終了要求を送信するには、次のようにします。

1.  [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)を呼び出して、 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体を割り当てます。
2.  終了ストリーム要求の URB をフォーマットします。 [**Urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体の**UrbPipeRequest**メンバーは[ **\_urb\_パイプ\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_pipe_request)構造体です。 メンバーを次のように入力します。
    -   [ **\_urb\_パイプ\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_pipe_request)の**Hdr**メンバーは、静的な\_ストリームを閉じる\_の urb\_関数である必要があります
    -   **PipeHandle**メンバーは、使用中の開いているストリームを含むエンドポイントへのハンドルである必要があります。

3.  [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)または[**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)を呼び出すことによって、URB を WDF 要求として送信します。

クローズハンドル要求は、クライアントドライバーによって既に開かれていたすべてのストリームを閉じます。 クライアントドライバーは、要求を使用してエンドポイント内の特定のストリームを閉じることはできません。

<a name="remarks"></a>注釈
-------

**静的ストリーム要求を送信するためのベストプラクティス**

USB ドライバースタックは、受信した URB に対して複数の検証を実行します。 検証エラーを回避するには、クライアントドライバーが次の点を考慮する必要があります。

-   ストリームをサポートしていないエンドポイントには、オープンストリームまたはクローズストリームの要求を送信しないでください。 [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) (WDM ドライバーの場合は[**USBD\_queryusbcapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))) を呼び出し、スタティックストリームのサポートを確認し、エンドポイントでサポートされている場合はストリーム要求だけを送信します。
-   サポートされているストリームの最大数を超えている (オープンストリームの) 数を要求したり、ストリームの数を指定せずに要求を送信したりしないでください。 USB ドライバースタックおよびデバイスのエンドポイントでサポートされているストリームの数に基づいて、ストリームの数を決定します。
-   既に開いているストリームがあるエンドポイントには、オープンストリーム要求を送信しないでください。
-   ストリームが開かれていないエンドポイントには、ストリームを閉じる要求を送信しないでください。
-   エンドポイントに対して静的ストリームを開いた後は、選択構成または選択インターフェイスの要求によって取得されたエンドポイントパイプハンドルを使用して、i/o 要求を送信しないでください。 これは、静的ストリームが閉じられている場合でも同様です。

**リセットおよび中止パイプ操作**

場合によっては、エンドポイントとの間の転送が失敗することがあります。 このようなエラーは、停止や停止など、エンドポイントまたはホストコントローラーのエラー状態が原因で発生する可能性があります。 エラー状態をクリアするために、クライアントドライバーはまず保留中の転送をキャンセルし、次にエンドポイントが関連付けられているパイプをリセットします。 保留中の転送を取り消すには、クライアントドライバーが abort パイプ要求を送信します。 パイプをリセットするには、クライアントドライバーがリセットパイプ要求を送信する必要があります。

ストリーム転送の場合は、一括エンドポイントに関連付けられている個々のストリームに対して、abort パイプとリセットパイプの両方の要求がサポートされていません。 特定のストリームパイプで転送が失敗した場合、ホストコントローラーは他のすべてのパイプの転送を停止します (他のストリームの場合)。 エラー状態から回復するには、クライアントドライバーが各ストリームへの転送を手動でキャンセルする必要があります。 次に、クライアントドライバーは、パイプハンドルを使用して一括エンドポイントに対して、リセットパイプ要求を送信する必要があります。 その要求については、クライアントドライバーは[ **\_urb\_パイプ\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_pipe_request)構造内のエンドポイントへのパイプハンドルを指定し、urb 関数 (**HDR**) を URB\_関数\_同期\_リセット @no_ に設定する必要があり_t_9_ パイプ\_と\_\_停止をクリアします。

## <a name="complete-example"></a>完全な例


次のコード例は、ストリームを開く方法を示しています。

```cpp
NTSTATUS
    OpenStreams (
    _In_ WDFDEVICE Device,
    _In_ WDFUSBPIPE Pipe)
{
    NTSTATUS status;

    PDEVICE_CONTEXT deviceContext;

    PPIPE_CONTEXT pipeContext;

    USHORT cStreams = 0;

    USBD_PIPE_HANDLE usbdPipeHandle;

    WDFMEMORY urbMemory = NULL;
    PURB      urb = NULL;

    PAGED_CODE();

    deviceContext =GetDeviceContext(Device);

    pipeContext = GetPipeContext (Pipe);

    if (deviceContext->MaxStreamsController == 0)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Static streams are not supported.");

        status = STATUS_NOT_SUPPORTED;

        goto Exit;

    }

    // If static streams are not supported, number of streams supported is zero. 

    if (pipeContext->MaxStreamsSupported == 0)
    {
        status = STATUS_DEVICE_CONFIGURATION_ERROR;

        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Static streams are not supported by the endpoint.");

        goto Exit;
    }

    // Determine the number of streams to open.
    // Compare the number of streams supported by the endpoint with the 
    // number of streams supported by the host controller, and choose the 
    // lesser of the two values. The deviceContext->MaxStreams value was 
    // obtained in a previous call to WdfUsbTargetDeviceQueryUsbCapability
    // that determined whether or not static streams is supported and
    // retrieved the maximum number of streams supported by the 
    // host controller. The device context stores the values for IN and OUT 
    // endpoints.

    // Allocate an array of USBD_STREAM_INFORMATION structures to store handles to streams.
    // The number of elements in the array is the number of streams to open.
    // The code snippet stores the array in its device context.


    cStreams = min(deviceContext->MaxStreamsController, pipeContext->MaxStreamsSupported);

    // Allocate an array of streams associated with the IN bulk endpoint
    // This array is released in CloseStreams.

    pipeContext->StreamInfo = (PUSBD_STREAM_INFORMATION) ExAllocatePoolWithTag (
        NonPagedPool,
        sizeof (USBD_STREAM_INFORMATION) * cStreams,
        USBCLIENT_TAG);

    if (pipeContext->StreamInfo == NULL)
    {
        status = STATUS_INSUFFICIENT_RESOURCES;

        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not allocate stream information array.");

        goto Exit;
    }

    RtlZeroMemory (pipeContext->StreamInfo,  
        sizeof (USBD_STREAM_INFORMATION) * cStreams);

    // Get USBD pipe handle from the WDF target pipe object. The client driver received the
    // endpoint pipe handles during device configuration.

    usbdPipeHandle = WdfUsbTargetPipeWdmGetPipeHandle (Pipe);


    // Allocate an URB for the open streams request. 
    // WdfUsbTargetDeviceCreateUrb returns the address of the 
    // newly allocated URB and the WDFMemory object that 
    // contains the URB.

    status = WdfUsbTargetDeviceCreateUrb (
        deviceContext->UsbDevice,
        NULL,
        &urbMemory,
        &urb);

    if (status != STATUS_SUCCESS)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not allocate URB for an open-streams request.");

        goto Exit;
    }

    // Format the URB for the open-streams request.
    // The UsbBuildOpenStaticStreamsRequest inline function formats the URB by specifying the
    // pipe handle to the entire bulk endpoint, number of streams to open, and the array of stream structures.

    UsbBuildOpenStaticStreamsRequest (
        urb,
        usbdPipeHandle,
        (USHORT)cStreams,
        pipeContext->StreamInfo);


    // Send the request synchronously.
    // Upon completion, the USB driver stack populates the array of with handles to streams.

    status = WdfUsbTargetPipeSendUrbSynchronously (
        Pipe,
        NULL,
        NULL,
        urb);

    if (status != STATUS_SUCCESS)
    {
        goto Exit;
    }

Exit:

    if (urbMemory)
    {
        WdfObjectDelete (urbMemory);
    }

    return status;

}
```

## <a name="related-topics"></a>関連トピック
[USB i/o 操作](usb-device-i-o.md)  



