---
title: 仮想 HID フレームワーク (VHF) を使用して HID ソースドライバーを作成する
description: HID データをオペレーティングシステムに報告する HID ソースドライバーの作成について説明します。
ms.assetid: 26964963-792F-4529-B4FC-110BF5C65B35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b3a5431ccaf2ffeb49bae33551c4f5b23ea3da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841549"
---
# <a name="write-a-hid-source-driver-by-using-virtual-hid-framework-vhf"></a>仮想 HID フレームワーク (VHF) を使用して HID ソースドライバーを作成する

**要約**

-   HID 読み取りレポートをオペレーティングシステムに送信するカーネルモードドライバーフレームワーク (KMDF) HID ソースドライバーを記述します。
-   VHF ドライバーを、仮想 HID デバイススタック内の HID ソースドライバーに対する下位フィルターとして読み込みます。

**適用対象**

-   Windows 10
-   HID デバイスのドライバー開発者

**重要な API**

-   [仮想 HID フレームワークのコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [仮想 HID フレームワークのメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [仮想 HID フレームワークの構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

HID データをオペレーティングシステムに報告する HID ソースドライバーの作成について説明します。

キーボード、マウス、ペン、タッチ、ボタンなどの HID 入力デバイスは、さまざまなレポートをオペレーティングシステムに送信して、デバイスの目的を理解し、必要なアクションを実行できるようにします。 レポートの形式は、 [hid コレクション](opening-hid-collections.md)と[hid usage](hid-usages.md)です。 デバイスは、これらのレポートをさまざまなトランスポートに[送信します。この](hid-over-usb.md)ようなレポートは、Windows によってサポートされています。このようなものは、Windows でサポートさ[れてい](hid-over-i2c-guide.md)ます。 場合によっては、トランスポートが Windows でサポートされていないか、レポートが実際のハードウェアに直接マップされていない可能性があります。 非 GPIO ボタンやセンサーのために、などの仮想ハードウェア用の別のソフトウェアコンポーネントによって送信される、HID 形式のデータストリームにすることができます。 たとえば、ゲームコントローラーとして動作し、PC にワイヤレスで送信される電話のデータを加速度計することを検討してください。 別の例では、コンピューターが UIBC プロトコルを使用して Miracast デバイスからリモート入力を受信できます。

以前のバージョンの Windows では、新しいトランスポート (実際のハードウェアまたはソフトウェア) をサポートするために、 [HID トランスポートミニドライバー](transport-minidrivers.md)を作成し、Microsoft が提供するインボックスクラスドライバー Hidclass にバインドする必要がありました。 クラス/ミニドライバーのペアでは、[最上位](top-level-collections.md)レベルのコレクションなど、HID コレクションが上位レベルのドライバーやユーザーモードアプリケーションに提供されています。 このモデルでは、困難な作業になる可能性があるミニドライバーを記述しています。

Windows 10 以降では、新しい仮想 HID フレームワーク (VHF) により、トランスポートミニドライバーを作成する必要がなくなります。 代わりに、KMDF または WDM プログラミングインターフェイスを使用して、HID ソースドライバーを作成できます。 フレームワークは、ドライバーによって使用されるプログラミング要素を公開する、Microsoft 提供のスタティックライブラリで構成されています。 また、1つまたは複数の子デバイスを列挙し、仮想 HID ツリーの構築と管理を進める、Microsoft が提供するインボックスドライバーも含まれています。

**注**  このリリースでは、VHF では、カーネルモードでのみ HID ソースドライバーがサポートされています。

このトピックでは、フレームワークのアーキテクチャ、仮想 HID デバイスツリー、および構成シナリオについて説明します。

## <a name="virtual-hid-device-tree"></a>仮想 HID デバイスツリー

このイメージの [デバイス] ツリーには、ドライバーとそれに関連付けられているデバイスオブジェクトが表示されます。

![仮想 hid デバイスツリー](images/vhf.png)

**HID ソースドライバー (お使いのドライバー)**

HID ソースドライバーは Vhfkm にリンクし、ビルドプロジェクトに Vhf を含めます。 ドライバーは、 [Windows ドライバーフレームワーク (WDF)](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)の一部である[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM) またはカーネルモードドライバーフレームワーク (kmdf) のいずれかを使用して書き込むことができます。 ドライバーは、フィルタードライバーまたは関数ドライバーとしてデバイススタックに読み込むことができます。

**VHF スタティックライブラリ (vhfkm)**

スタティックライブラリは、windows 10 用の Windows Driver Kit (WDK) に含まれています。 ライブラリは、HID ソースドライバーによって使用されるルーチンやコールバック関数などのプログラミングインターフェイスを公開します。 ドライバーが関数を呼び出すと、スタティックライブラリは要求を処理する VHF ドライバーに要求を転送します。

**VHF ドライバー (Vhf)**

Microsoft が提供するインボックスドライバー。 このドライバーは、HID ソースデバイススタックのドライバーの下に、下位のフィルタードライバーとして読み込む必要があります。 VHF ドライバーは、子デバイスを動的に列挙し、HID ソースドライバーによって指定された1つまたは複数の HID デバイス用に物理デバイスオブジェクト (PDO) を作成します。 また、列挙された子デバイスの HID トランスポートミニドライバー機能も実装します。

**HID クラスドライバーのペア (Hidclass、Mshidkmdf)**

Hidclass/Mshidkmdf ペアは、実際の HID デバイスのコレクションを列挙する方法と同様に、[最上位レベルのコレクション (TLC)](top-level-collections.md)を列挙します。 HID クライアントは、実際の HID デバイスと同様に、TLCs の要求と使用を続行できます。 このドライバーペアは、関数ドライバーとしてデバイススタックにインストールされます。

**注**  一部のシナリオでは、hid クライアントが hid データのソースを特定する必要がある場合があります。 たとえば、システムには組み込みのセンサーがあり、同じ種類のリモートセンサーからデータを受信します。 システムでは、1つのセンサーをより信頼性の高いものにすることができます。 システムに接続されている2つのセンサーを区別するために、HID クライアントは TLC のコンテナー ID を照会します。 この場合、HID ソースドライバーはコンテナー ID を提供できます。これは、VHF によって仮想 HID デバイスのコンテナー ID として報告されます。

**HID クライアント (アプリケーション)**

HID デバイススタックによって報告される TLCs を照会して使用します。

## <a name="header-and-library-requirements"></a>ヘッダーとライブラリの要件

この手順では、ヘッドセットボタンをオペレーティングシステムに報告する単純な HID ソースドライバーを記述する方法について説明します。 この場合、このコードを実装するドライバーは、VHF を使用して HID ソースレポートヘッドセットボタンとして機能するように変更された既存の KMDF オーディオドライバーにすることができます。

1.  Vhf をインクルードします。これは、Windows 10 用の WDK に含まれています。
2.  WDK に含まれている vhfkm にリンクします。
3.  デバイスがオペレーティングシステムに報告する HID レポート記述子を作成します。 この例では、HID レポート記述子にヘッドセットボタンが記述されています。 このレポートでは、HID 入力レポート (8 ビット (1 バイト)) が指定されています。 最初の3つのビットは、ヘッドセットの中央、ボリュームアップ、およびボリュームダウンのボタンです。 残りのビットは使用されません。

```cpp
UCHAR HeadSetReportDescriptor[] = {
    0x05, 0x01,         // USAGE_PAGE (Generic Desktop Controls)
    0x09, 0x0D,         // USAGE (Portable Device Buttons)
    0xA1, 0x01,         // COLLECTION (Application)
    0x85, 0x01,         //   REPORT_ID (1)
    0x05, 0x09,         //   USAGE_PAGE (Button Page)
    0x09, 0x01,         //   USAGE (Button 1 - HeadSet : middle button)
    0x09, 0x02,         //   USAGE (Button 2 - HeadSet : volume up button)
    0x09, 0x03,         //   USAGE (Button 3 - HeadSet : volume down button)
    0x15, 0x00,         //   LOGICAL_MINIMUM (0)
    0x25, 0x01,         //   LOGICAL_MAXIMUM (1)
    0x75, 0x01,         //   REPORT_SIZE (1)
    0x95, 0x03,         //   REPORT_COUNT (3)
    0x81, 0x02,         //   INPUT (Data,Var,Abs)
    0x95, 0x05,         //   REPORT_COUNT (5)
    0x81, 0x03,         //   INPUT (Cnst,Var,Abs)
    0xC0,               // END_COLLECTION
};
```

## <a name="create-a-virtual-hid-device"></a>仮想 HID デバイスを作成する

[**VHF\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhf_config_init)マクロを呼び出し、 [**VhfCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfcreate)メソッドを呼び出すことによって、 [**VHF\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)構造体を初期化します。 ドライバーは、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)呼び出しの後 (通常はドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数で)、 **VhfCreate**をパッシブ\_レベルで呼び出す必要があります。

[**VhfCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfcreate)の呼び出しでは、ドライバーは、非同期的に処理する必要がある操作や、デバイス情報 (ベンダ/製品 id) を設定する操作など、特定の構成オプションを指定できます。

たとえば、アプリケーションが TLC を要求したとします。 HID クラスドライバーペアがその要求を受信すると、ペアは要求の種類を決定し、適切な[HID ミニドライバー IOCTL](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)要求を作成して VHF に転送します。 VHF は、IOCTL 要求を取得するときに、要求を処理するか、HID ソースドライバーを使用して処理するか\_サポートされていない状態\_要求を完了することができます。

VHF は、これらの Ioctl を処理します。

-   [**IOCTL\_HID\_\_文字列を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_string)
-   [**IOCTL\_HID\_\_デバイス\_属性を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_device_attributes)
-   [**IOCTL\_HID\_\_デバイス\_記述子を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_device_descriptor)
-   [**IOCTL\_HID\_\_レポート\_記述子を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_report_descriptor)

要求が**Getfeature**、 **setfeature**、 **WriteReport**、または**getinputreport**で、HID ソースドライバーが対応するコールバック関数を登録した場合、VHF はコールバック関数を呼び出します。 その関数内で、hid ソースドライバーは hid 仮想デバイスの HID データを取得または設定できます。 ドライバーでコールバックが登録されていない場合、VHF はステータスステータスの要求を完了し\_\_サポートされていません。

VHF は、これらの Ioctl に対して、HID ソースドライバーによって実装されたイベントコールバック関数を呼び出します。

-   [**IOCTL\_HID\_読み取り\_レポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_read_report)

    HID 入力レポートを取得するためにバッファーを送信するときに、ドライバーがバッファリングポリシーを処理する必要がある場合は、 [*EvtVhfReadyForNextReadReport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_ready_for_next_read_report)を実装し、 **EvtVhfAsyncOperationGetInputReport**メンバーにポインターを指定する必要があります。 詳細については、「 [HID 入力レポートを送信する](#submit-the-hid-input-report)」を参照してください。

-   [**Ioctl\_hid\_\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_feature)または[ **IOCTL\_HID\_設定\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_feature)

    ドライバーが HID 機能レポートを非同期に取得または設定する必要がある場合、ドライバーは[*EvtVhfAsyncOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_async_operation)関数を実装し、 **EvtVhfAsyncOperationGetFeature**の get または**set 実装関数へのポインターを指定する必要があります。** [**VHF\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)の EvtVhfAsyncOperationSetFeature メンバー。

-   [**IOCTL\_HID\_\_入力\_レポートを取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_input_report)

    ドライバーが HID 入力レポートを非同期に取得する必要がある場合、ドライバーは[*EvtVhfAsyncOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_async_operation)関数を実装し、 [**VHF\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)の**EvtVhfAsyncOperationGetInputReport**メンバーにある関数へのポインターを指定する必要があります。

-   [**IOCTL\_HID\_書き込み\_レポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_write_report)

    ドライバーが HID 入力レポートを非同期的に書き込む必要がある場合、ドライバーは[*EvtVhfAsyncOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_async_operation)関数を実装し、 [**VHF\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)の**EvtVhfAsyncOperationWriteReport**メンバー内の関数へのポインターを指定する必要があります。

その他の[HID ミニドライバー IOCTL](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)では、VHF はサポートされて\_いない状態\_要求を完了します。

仮想 HID デバイスは、 [**VhfDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete)を呼び出すことによって削除されます。 ドライバーが仮想 HID デバイスにリソースを割り当てた場合、 [*EvtVhfCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup)コールバックが必要です。 ドライバーは、 *EvtVhfCleanup*関数を実装し、 [**VHF\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)の**EvtVhfCleanup**メンバーでその関数へのポインターを指定する必要があります。 *EvtVhfCleanup*は、 **VhfDelete**の呼び出しが完了する前に呼び出されます。 詳細については、「[仮想 HID デバイスを削除する](#delete-the-virtual-hid-device)」を参照してください。

**注**  非同期操作が完了した後、ドライバーは[**VhfAsyncOperationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfasyncoperationcomplete)を呼び出して操作の結果を設定する必要があります。 イベントコールバックから、またはコールバックから戻った後に、メソッドを呼び出すことができます。

```cpp
NTSTATUS
VhfSourceCreateDevice(
_Inout_ PWDFDEVICE_INIT DeviceInit
)

{
    WDF_OBJECT_ATTRIBUTES   deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    VHF_CONFIG vhfConfig;
    WDFDEVICE device;
    NTSTATUS status;

    PAGED_CODE();

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);
    deviceAttributes.EvtCleanupCallback = VhfSourceDeviceCleanup;

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status))
    {
        deviceContext = DeviceGetContext(device);

        VHF_CONFIG_INIT(&vhfConfig,
            WdfDeviceWdmGetDeviceObject(device),
            sizeof(VhfHeadSetReportDescriptor),
            VhfHeadSetReportDescriptor);

        status = VhfCreate(&vhfConfig, &deviceContext->VhfHandle);

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, "VhfCreate failed %!STATUS!", status);
            goto Error;
        }

        status = VhfStart(deviceContext->VhfHandle);
        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, "VhfStart failed %!STATUS!", status);
            goto Error;
        }

    }

Error:
    return status;
}
```

## <a name="submit-the-hid-input-report"></a>HID 入力レポートを送信する

[**VhfReadReportSubmit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfreadreportsubmit)を呼び出して、HID 入力レポートを送信します。

通常、HID デバイスは、割り込みを介して入力レポートを送信することによって、状態の変化に関する情報を送信します。 たとえば、ヘッドセットデバイスは、ボタンの状態が変化したときにレポートを送信する場合があります。 このようなイベントでは、ドライバーの割り込みサービスルーチン (ISR) が呼び出されます。 このルーチンでは、ドライバーは、入力レポートを処理して VHF に送信する遅延プロシージャ呼び出し (DPC) をスケジュールすることがあります。これにより、情報がオペレーティングシステムに送信されます。 既定では、VHF によってレポートがバッファーされます。 HID ソースドライバーは、表示されているときに HID 入力レポートの送信を開始できます。 これにより、HID ソースドライバーが複雑な同期を実装する必要がなくなります。

HID ソースドライバーは、保留中のレポートに対してバッファリングポリシーを実装することによって、入力レポートを送信できます。 バッファーの重複を回避するために、HID ソースドライバーは[*EvtVhfReadyForNextReadReport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_ready_for_next_read_report) callback 関数を実装し、VHF がこのコールバックを呼び出したかどうかを追跡できます。 以前に呼び出されていた場合、HID ソースドライバーは[**VhfReadReportSubmit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfreadreportsubmit)を呼び出してレポートを送信できます。 **VhfReadReportSubmit**を再度呼び出す前に、 *EvtVhfReadyForNextReadReport*が呼び出されるまで待機する必要があります。

```cpp
VOID
MY_SubmitReadReport(
    PMY_CONTEXT  Context,
    BUTTON_TYPE  ButtonType,
    BUTTON_STATE ButtonState
    )
{
    PDEVICE_CONTEXT deviceContext = (PDEVICE_CONTEXT)(Context);

    if (ButtonState == ButtonStateUp) {
        deviceContext->VhfHidReport.ReportBuffer[0] &= ~(0x01 << ButtonType);
    } else {
        deviceContext->VhfHidReport.ReportBuffer[0] |=  (0x01 << ButtonType);
    }

    status = VhfSubmitReadReport(deviceContext->VhfHandle, &deviceContext->VhfHidReport);

    if (!NT_SUCCESS(status)) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,"VhfSubmitReadReport failed %!STATUS!", status);
    }
}
```

## <a name="delete-the-virtual-hid-device"></a>仮想 HID デバイスを削除します。

[**VhfDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete)を呼び出して、仮想 HID デバイスを削除します。

[**VhfDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete)は、Wait パラメーターを指定することによって、同期または非同期で呼び出すことができます。 同期呼び出しの場合、メソッドは、デバイスオブジェクトの[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)など、パッシブ\_レベルで呼び出す必要があります。 **VhfDelete**は、仮想 HID デバイスを削除した後にを返します。 ドライバーが非同期に**VhfDelete**を呼び出した場合は、直ちに制御が戻り、削除操作の完了後に VHF が[*EvtVhfCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup)を呼び出します。 メソッドは、最大ディスパッチ\_レベルで呼び出すことができます。 この場合、ドライバーは、以前に[**VhfCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfcreate)を呼び出したときに*EvtVhfCleanup* callback 関数を登録し、実装する必要があります。 HID ソースドライバーが仮想 HID デバイスを削除する場合のイベントのシーケンスを次に示します。

1.  HID ソースドライバーは、VHF への呼び出しの開始を停止します。
2.  HID ソースは*Wait*を FALSE に設定して[**VhfDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete)を呼び出します。
3.  VHF は、HID ソースドライバーによって実装されているコールバック関数の呼び出しを停止します。
4.  VHF は、デバイスが PnP マネージャーに存在しないと報告を開始します。 この時点で、VhfDelete の呼び出しでが返される場合があります。
5.  デバイスが不足しているデバイスとして報告された場合、VHF は、HID ソースドライバーの実装が登録されている場合は[*EvtVhfCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup)を呼び出します。
6.  [*EvtVhfCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup)が返された後、VHF はクリーンアップを実行します。

```cpp
VOID
VhfSourceDeviceCleanup(
_In_ WDFOBJECT DeviceObject
)
{
    PDEVICE_CONTEXT deviceContext;

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    deviceContext = DeviceGetContext(DeviceObject);

    if (deviceContext->VhfHandle != WDF_NO_HANDLE)
    {
        VhfDelete(deviceContext->VhfHandle, TRUE);
    }

}
```

## <a name="install-the-hid-source-driver"></a>HID ソースドライバーをインストールする

HID ソースドライバーをインストールする INF ファイルで、 [**AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して、VHF を hid ソースドライバーの下位フィルタードライバーとして宣言していることを確認します。

```cpp
[HIDVHF_Inst.NT.HW]
AddReg = HIDVHF_Inst.NT.AddReg

[HIDVHF_Inst.NT.AddReg]
HKR,,"LowerFilters",0x00010000,"vhf"
```

## <a name="related-topics"></a>関連トピック
[ヒューマンインターフェイスデバイス](https://developer.microsoft.com/windows/hardware)

