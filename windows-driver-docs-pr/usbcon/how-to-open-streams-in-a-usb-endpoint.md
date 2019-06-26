---
Description: このトピックでは、静的なストリームの機能について説明し、USB クライアント ドライバーが開くし、USB 3.0 デバイスの一括エンドポイントでのストリームを閉じる方法について説明します。
title: USB バルク エンドポイントにおける静的ストリームのオープン/クローズ方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2346c810a9405d3d230a97da4c98f798bd6650c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386253"
---
# <a name="how-to-open-and-close-static-streams-in-a-usb-bulk-endpoint"></a>USB バルク エンドポイントにおける静的ストリームのオープン/クローズ方法


このトピックで説明*静的ストリーム機能*と USB クライアント ドライバーが開くし、USB 3.0 デバイスの一括エンドポイントでのストリームを閉じる方法について説明します。

USB 2.0 およびそれ以前のデバイスでは、一括エンドポイントは送信またはエンドポイントの 1 つのデータ ストリームを受信できます。 一括エンドポイントでは、USB 3.0 デバイスのエンドポイントを介して複数のデータ ストリームを送受信する機能があります。

Windows 8 の Microsoft 提供の USB ドライバー スタックは、複数のストリームをサポートします。 これにより、USB 3.0 デバイスの一括エンドポイントに関連付けられた各ストリームに独立した I/O 要求を送信するためのクライアント ドライバーができます。 異なるストリームへの要求はシリアル化されません。

クライアント ドライバーの場合は、ストリームは、特性のセットが同じ複数の論理エンドポイントを表します。 に特定のストリームを要求を送信するには、は、クライアント ドライバーそのストリームへのハンドル (エンドポイントのパイプ ハンドルに似ています) 必要があります。 ストリームへの I/O 要求の URB は、一括エンドポイントに対する I/O 要求を URB に似ています。 唯一の違いは、パイプ ハンドルです。 ストリームに、I/O 要求を送信するには、は、ドライバーは、ストリームにパイプ ハンドルを指定します。

デバイスの構成時に、クライアント ドライバーは、選択構成要求と、必要に応じて選択インターフェイス要求を送信します。 それらの要求では、一連のインターフェイスのアクティブな設定で定義されているエンドポイントへのパイプ ハンドルを取得します。 ストリームをサポートするエンドポイントへの I/O 要求を送信するエンドポイントのパイプ ハンドルを使用できますに、*既定のストリーム*(最初のストリーム)、ドライバーが (後述) のストリームを開いたとき。

クライアント ドライバーは、既定のストリーム以外のストリームに要求を送信する場合、ドライバーを開くし、すべてのストリームへのハンドルを取得する必要があります。 これを行うには、クライアント ドライバーの送信、*オープン ストリーム要求*を開くストリームの数を指定することで。 ドライバーの完了後、クライアントにストリームを使用して、ドライバー閉じることができます必要に応じてそれらを送信して、*閉じるストリーム要求*します。

カーネル モード ドライバー フレームワーク (KMDF)、静的なストリームが本質的にサポートされていません。 クライアント ドライバーでは、Windows Driver Model (WDM) スタイルを開いて閉じるストリーム翻訳を送信する必要があります。 このトピックでは、書式を設定し、それらの翻訳を送信する方法について説明します。 ユーザー モード ドライバー フレームワーク (UMDF) のクライアント ドライバーは、静的ストリームの機能を使用できません。

このトピックの内容としてラベル付けされている次の事項**WDM ドライバー**します。 これらのノートには、ストリームの要求を送信する必要がある WDM ベースの USB クライアント ドライバーがについて説明します。

### <a name="prerequisites"></a>前提条件

クライアント ドライバーは開くことや、ストリームを閉じる、前に、ドライバーが表示される場合があります。

- 呼ばれる、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッド。

  メソッドには、USBD にクライアント コントラクト バージョンが必要です。\_クライアント\_コントラクト\_バージョン\_602 します。 そのバージョンを指定することで、クライアント ドライバーは、一連のルールに従う必要があります。 詳細については、次を参照してください。[ベスト プラクティス。翻訳を使用して](usb-client-driver-contract-in-windows-8.md)します。

  呼び出しでは、フレームワークの USB ターゲット デバイス オブジェクトを識別する WDFUSBDEVICE ハンドルを取得します。 そのハンドルがストリームを開いて、後続の呼び出しを行うために必要です。 通常、クライアント ドライバーに自らを登録、ドライバーの[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベント コールバック ルーチン。

  <strong>WDM ドライバー: * * を呼び出す、 [ </strong>USBD\_CreateHandle * *](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)ルーチンは USB ドライバー スタックと、ドライバーの登録のため、USBD ハンドルを取得します。

- デバイスを構成し、ストリームをサポートする一括エンドポイントへの WDFUSBPIPE パイプ ハンドルを取得します。 パイプ ハンドルを取得するには、呼び出し、 [ **WdfUsbInterfaceGetConfiguredPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)メソッドを選択した構成でインターフェイスの現在の代替設定します。

  \* * WDM ドライバー: * * 構成を選択または選択インターフェイスの要求を送信することによって USBD パイプ ハンドルを取得します。 詳細については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。

<a name="instructions"></a>手順
------------

### <a name="how-to-open-static-streams"></a>静的なストリームを開く方法

<a href="" id="open-streams"></a>
1. 基になる USB ドライバー スタックとコント ローラーのホストが呼び出すことによって静的ストリームの機能をサポートするかどうかを確認、 [ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)メソッド。 通常、クライアント ドライバーがドライバーのルーチンを呼び出す[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベント コールバック ルーチン。

   <strong>WDM ドライバー: * * を呼び出す、 [ </strong>USBD\_QueryUsbCapability<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406230>)ルーチン。ドライバーのデバイスの起動のルーチンで使用したい機能のドライバー クエリでは通常、([</strong>IRP\_MN\_開始\_デバイス<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff551749>))。コード例では、次を参照してください。 * * USBD\_QueryUsbCapability</strong>します。

   次の情報を提供します。

   - 以前の呼び出しで取得された USB デバイス オブジェクトを識別するハンドル[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)、クライアント ドライバーの登録をします。

     <strong>WDM ドライバー: * * を前の呼び出しで取得された USBD ハンドルを渡す[ </strong>USBD\_CreateHandle * *](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)します。

     クライアント ドライバーは、特定の機能を使用する場合、ドライバーはドライバー スタックとホスト コント ローラーが、機能をサポートするかどうかを判断する基礎となる USB ドライバー スタックを最初にクエリする必要があります。 機能がサポートされている場合、そのドライバーは、機能を使用して要求を送信する必要があります。 一部の要求では、(手順 5. で説明します)、ストリームの機能など、翻訳が必要です。 これらの要求のクエリ機能を同じハンドルを使用して翻訳を割り当てることを確認します。 ドライバー スタックでは、ハンドルを使用して、ドライバーが使用できる、サポートされる機能を追跡するためです。

     たとえば、USBD を入手した場合\_処理 (呼び出して[ **USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle))、ドライバー スタックを呼び出すことによってクエリ[ **USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))、呼び出すことによって、URB を割り当てると[ **USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_urballocate)します。 同じ USBD を渡す\_これら両方の呼び出しでのハンドル。

     KMDF のメソッドを呼び出した場合[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)と[ **WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)、同じ指定フレームワークの対象オブジェクトのメソッド呼び出しへ WDFUSBDEVICE のハンドルします。

   - GUID に割り当てられた GUID\_USB\_機能\_静的\_ストリーム。
   - 出力バッファー (USHORT へのポインター)。 完了すると、バッファーは、ホスト コント ローラーでサポートされているストリーム (エンドポイント) ごとの最大数が入力されます。
   - 出力バッファーの長さ、(バイト単位)。 ストリームの長さは、`sizeof (USHORT)`します。

2. 返される NTSTATUS 値を評価します。 ルーチンが正常に完了すると、ステータスを返します\_成功すると、機能がサポートされている静的なストリーム。 それ以外の場合、メソッドは、適切なエラー コードを返します。
3. 開くストリームの数を決定します。 開くことができるストリームの最大数は、によって制限されます。
   -   ホスト コント ローラーでサポートされているストリームの最大数。 数がによって受信される[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) (WDM ドライバーについて[ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)))、呼び出し元が指定の出力バッファーにします。 Microsoft 提供の USB ドライバー スタックは、最大 255 個のストリームをサポートします。 **WdfUsbTargetDeviceQueryUsbCapability**ストリームの数を計算する際に考慮する制限がかかります。 メソッドは、255 より大きい値を返しません。
   -   デバイスのエンドポイントでサポートされているストリームの最大数。 その数を取得するには、エンドポイント コンパニオンの記述子を検査します (を参照してください[ **USB\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)でUsbspec.h)。 エンドポイント コンパニオンの記述子を取得するには、構成記述子を解析する必要があります。 構成記述子を取得するには、クライアント ドライバーを呼び出す必要があります、 [ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)メソッド。 ヘルパー ルーチンを使用する必要があります[ **USBD\_ParseConfigurationDescriptorEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)と[ **USBD\_ParseDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_parsedescriptors). コード例では、関数で RetrieveStreamInfoFromEndpointDesc という名前の例を参照してください[USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

   ストリームの最大数を調べるには、ホスト コント ローラーと、エンドポイントでサポートされている 2 つの値のうちの小さい方を選択します。
4. 配列を割り当てる[ **USBD\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_stream_information)と構造体*n* 、要素、 *n*は開くストリームの数。 クライアント ドライバーはドライバーが完了した後は、この配列を解放する必要がストリームを使用します。
5. 開くストリームの要求を呼び出すことによって、URB を割り当て、 [ **WdfUsbTargetDeviceCreateUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッド。 メソッドは、WDF のメモリ オブジェクトとのアドレスを取得呼び出しが正常に完了した場合、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb) USB ドライバー スタックが割り当てられる構造体。

   <strong>WDM ドライバー: * * を呼び出す、 [ </strong>USBD\_UrbAllocate * *](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)ルーチン。

6. オープン ストリーム要求の URB の書式を設定します。 URB を使用して、 [  **\_URB\_オープン\_静的\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_open_static_streams)要求を定義する構造体。 URB の書式を設定する必要があります。
   -   エンドポイントへの USBD パイプ ハンドル。 呼び出して USBD パイプ ハンドルを取得するには、WDF パイプ オブジェクトがあれば、 [ **WdfUsbTargetPipeWdmGetPipeHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)メソッド。
   -   (手順 4. で作成された) ストリーム配列
   -   ポインター、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)構造 (手順 5. で作成) します。

   URB の書式を設定するには、呼び出す[ **UsbBuildOpenStaticStreamsRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildopenstaticstreamsrequest)パラメーター値として必要な情報を渡します。 ストリームの数を指定することを確認**UsbBuildOpenStaticStreamsRequest**がサポートされているストリームの最大数を超えていません。
7. WDF の要求オブジェクトとして呼び出すことによって、URB を送信、 [ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド。 要求を同期的に送信する、 [ **WdfUsbTargetDeviceSendUrbSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)メソッド代わりにします。

   \* * WDM ドライバー: * *、IRP URB を関連付けるし、USB ドライバー スタックに IRP を送信します。 詳細については、次を参照してください。 [、URB を送信する方法](send-requests-to-the-usb-driver-stack.md)します。

8. 要求が完了した後は、要求の状態を確認します。

   USB ドライバー スタックには、要求が失敗した場合、URB ステータスに関連するエラー コードが含まれます。 いくつかの一般的なエラー状態は、「解説」で説明します。

(IRP または WDF 要求オブジェクト) の要求の状態が USBD を示している場合\_状態\_成功すると、要求が正常に完了しました。 配列を検査[ **USBD\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_stream_information)完了時に受信した構造体。 配列には、要求されたストリームに関する情報が格納されます。 USB ドライバー スタックは、ハンドルなどのストリームについては、配列内の各構造を設定します (USBD として受信した\_パイプ\_処理)、ストリームの識別子、および転送サイズの最大数。 ストリームは、データを転送するようになりました。

オープン ストリーム要求の場合、URB および配列を割り当てる必要があります。 クライアント ドライバーは呼び出すことによって、URB を解放する必要があります、 [ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)関連付けられている WDF メモリ オブジェクト、開いているストリームを要求の完了後のメソッド。 ドライバーで要求を送信同期的に呼び出す場合[ **WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)、メソッドが返された後に、WDF メモリ オブジェクトを解放が必要があります。 呼び出してにかどうか、クライアント ドライバーが要求を非同期的に送信[ **WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)ドライバーは WDF のメモリ オブジェクトに関連付けられているドライバー実装完了ルーチンをリリースする必要があります、要求。

クライアント ドライバーがストリームを使用する完成したかが I/O 要求の保存後、ストリームの配列を解放できます。 このトピックに含まれるコードの例では、ドライバーは、デバイス コンテキストでストリームの配列を格納します。 ドライバーは、削除、デバイス オブジェクトを解放する前に、デバイス コンテキストを解放します。

### <a name="how-to-transfer-data-to-a-particular-stream"></a>特定のストリームにデータを転送する方法

に特定のストリームをデータの転送要求を送信するには、WDF の要求オブジェクトを必要があります。 通常、クライアント ドライバーでは、WDF 要求オブジェクトを割り当てる必要はありません。 I/O マネージャーは、アプリケーションから要求を受信すると、I/O マネージャーには、要求の IRP が作成されます。 その IRP がフレームワークによって受け取られます。 フレームワークは、WDF 要求オブジェクトを表す IRP を割り当てます。 その後は、フレームワークは、クライアント ドライバーを WDF 要求オブジェクトを渡します。 クライアント ドライバーは、要求オブジェクトを関連付ける URB データ転送し、USB ドライバー スタックに送信します。

クライアント ドライバーでは、フレームワークから WDF 要求オブジェクトを受信しないと、要求を非同期的に送信する必要がある場合、ドライバーが呼び出すことによって WDF 要求オブジェクトを割り当てる必要があります、 [ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)メソッド。 呼び出すことによって、新しいオブジェクトを書式設定[ **WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)、呼び出すことによって、要求を送信したり[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend).

同期の場合は、WDF 要求オブジェクトを渡すことは省略可能です。

ストリームにデータを転送するには、翻訳を使用する必要があります。 呼び出すことによって、URB の書式を設定する必要があります[ **WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)します。

次の WDF メソッドは*いない*ストリームのサポートします。

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)
-   [**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

次の手順では、クライアント ドライバーでは、framework からの要求オブジェクトが受信を前提としています。

1.  呼び出すことによって、URB を割り当てる[ **WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)します。 このメソッドは、新しく割り当てられた URB を含む WDF メモリ オブジェクトを割り当てます。 クライアント ドライバーは、I/O 要求ごとに、URB を割り当てまたは、URB を割り当てるし、同じ種類の要求の再利用を選択できます。
2.  呼び出して一括転送する場合、URB を書式設定[ **UsbBuildInterruptOrBulkTransferRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbbuildinterruptorbulktransferrequest)します。 *PipeHandle*パラメーター、ストリームを識別するハンドルを指定します。 ストリームのハンドルで説明されている、前回の要求で取得した、[静的ストリームを開く方法](#open-streams)セクション。
3.  呼び出すことによって、WDF 要求オブジェクトを書式設定、 [ **WdfUsbTargetPipeFormatRequestForUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)メソッド。 呼び出しでは、データ転送 URB を含む、WDF メモリ オブジェクトを指定します。 メモリ オブジェクトは、手順 1. で割り当てられました。
4.  URB をいずれかを呼び出した WDF 要求として送信[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)または[ **WdfUsbTargetPipeSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipesendurbsynchronously)します。 呼び出す場合**WdfRequestSend**、呼び出すことによって完了ルーチンを指定する必要があります[ **WdfRequestSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)クライアント ドライバーを取得できるときに通知します非同期操作が完了しました。 完了ルーチンでは、データ転送の URB を解放する必要があります。

<strong>WDM ドライバー: * * を呼び出して、URB を割り当てる[ </strong>USBD\_UrbAllocate<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)し、書式を一括転送する場合 (を参照してください[ </strong> \_URB\_一括\_または\_INTERRUPT\_転送<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff540352>))。呼び出すことができます、URB の書式を設定する[ </strong>UsbBuildInterruptOrBulkTransferRequest<strong> ](<https://msdn.microsoft.com/library/windows/hardware/ff538953>)または URB 構造を手動で書式設定します。URB の **UrbBulkOrInterruptTransfer.PipeHandle でストリームを識別するハンドルを指定</strong>メンバー。

### <a name="how-to-close-static-streams"></a>静的なストリームを閉じる方法

クライアント ドライバーはドライバーが完了したらストリームを閉じることができますを使用します。 ただし、閉じるストリームの要求は省略可能です。 USB ドライバー スタックは、ストリームに関連付けられているエンドポイントが構成解除すると、すべてのストリームを閉じます。 代替の構成またはインターフェイスを選択すると、エンドポイントが構成解除、デバイスが削除されると、具合です。 クライアント ドライバーは、ドライバーは、異なる数のストリームを開く必要がある場合、ストリームを閉じる必要があります。 閉じるストリームの要求を送信するには。

1.  割り当て、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)呼び出して構造[ **WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)します。
2.  閉じるストリーム要求の URB の書式を設定します。 **UrbPipeRequest**のメンバー、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)構造体は、 [  **\_URB\_パイプ\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_pipe_request)構造体。 次のように、そのメンバーを入力します。
    -   **Hdr**のメンバー [  **\_URB\_パイプ\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_pipe_request) URB 必要があります\_関数\_閉じる\_静的\_ストリーム
    -   **PipeHandle**メンバーは使用中で開いているストリームを含むエンドポイントを識別するハンドルである必要があります。

3.  URB をいずれかを呼び出した WDF 要求として送信[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)または[ **WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)します。

閉じるハンドルの要求は、クライアント ドライバーによって開かれた以前のすべてのストリームを閉じます。 クライアント ドライバーでは、エンドポイントで特定のストリームを閉じる要求を使用できません。

<a name="remarks"></a>コメント
-------

**ストリームの静的な要求を送信するためのベスト プラクティス**

USB ドライバー スタックは、受信した URB に対して、検証の数を実行します。 検証エラーを避けるためには、クライアント ドライバーは、次の点を考慮する必要があります。

-   ストリームがサポートされていないエンドポイントには、オープン ストリームまたは閉じるストリームの要求を送信しません。 呼び出す[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) (WDM ドライバーについて[ **USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))) する静的ストリームをサポートし、エンドポイントには、それらがサポートしている場合にのみストリームの要求を送信を決定します。
-   サポートされているストリームの最大数を超える (ストリームを開く) の番号を要求したり、ストリームの数を指定せず、要求を送信しないでください。 USB ドライバー スタックと、デバイスのエンドポイントでサポートされているストリームの数に基づいてストリームの数を決定します。
-   既に開いているストリームを持つエンドポイントには、オープン ストリーム要求を送信しません。
-   開いているストリームがないエンドポイントには、閉じるストリームの要求を送信できません。
-   静的ストリーム エンドポイントに対して開いている場合、エンドポイントのパイプを使用して、I/O 要求を処理する送信しない後は、選択構成または選択インターフェイス要求を通じて取得されました。 これは、静的なストリームが閉じられた場合でも当てはまります。

**リセットし、パイプ操作の中止**

エンドポイントとの間の転送は失敗します。 このようなエラーでは、エンドポイントまたはホスト コント ローラーで、停止など、エラー状態が発生したり、条件を停止することができます。 エラー状態をクリアするには、クライアント ドライバーは、最初保留中の転送をキャンセルし、エンドポイントが関連付けられているパイプをリセットします。 保留中の転送をキャンセルするには、クライアント ドライバーは、中止パイプ要求を送信できます。 パイプをリセットするには、クライアント ドライバーはリセット パイプ要求を送信する必要があります。

ストリームの転送を中止パイプとリセット パイプ要求の両方はサポートされていません一括エンドポイントに関連付けられている個別のストリーム。 特定のストリームのパイプでの転送に失敗した場合、ホスト コント ローラーは、(その他のストリーム) の他のすべてのパイプで転送を停止します。 にエラー状態から回復するには、クライアント ドライバーは、各ストリームへの転送を手動で取り消す必要があります。 次に、クライアント ドライバーでは、一括エンドポイントへのパイプ ハンドルを使用してリセット パイプ要求を送信する必要があります。 クライアント ドライバーは、その要求のエンドポイントにパイプ ハンドルを指定する必要があります、 [  **\_URB\_パイプ\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_pipe_request)構造体であり (URB関数の設定**Hdr.Function**) URB に\_関数\_同期\_リセット\_パイプ\_AND\_クリア\_停止します。

## <a name="complete-example"></a>完全な例


次のコード例では、ストリームを開く方法を示します。

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
[USB I/O 操作](usb-device-i-o.md)  



