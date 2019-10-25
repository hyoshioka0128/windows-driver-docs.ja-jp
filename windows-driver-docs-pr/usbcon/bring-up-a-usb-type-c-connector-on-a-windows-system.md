---
Description: USB タイプ C コネクタと、コネクタドライバーの予期される動作を管理する USB コネクタマネージャー (UCM) について説明します。
title: USB Type-C コネクタ ドライバーを記述する
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2bf534db58790a01bd8712161607a6dc0dd9a91d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842408"
---
# <a name="write-a-usb-type-c-connector-driver"></a>USB Type-C コネクタ ドライバーを記述する

次のシナリオでは、USB タイプ C コネクタドライバーを記述する必要があります。

* USB タイプ C ハードウェアに、電力配信 (PD) のステートマシンを処理する機能がある場合。 それ以外の場合は、USB タイプ C ポートコントローラードライバーを記述することを検討してください。 詳細については、「 [Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md)」を参照してください。

* ハードウェアに埋め込みコントローラーがない場合。 それ以外の場合は、Microsoft が提供するインボックスドライバーである UcmUcsi を読み込みます。 ACPI トランスポートについては、「 [ucsi ドライバー](ucsi.md)」を参照してください。または、非 acpi トランスポート用に[ucsi クライアントドライバーを作成](write-a-ucsi-driver.md)してください。

## <a name="summary"></a>概要

* クラス拡張とクライアントドライバーによって使用される UCM オブジェクト
* UCM クラス拡張機能によって提供されるサービス
* クライアントドライバーの予期される動作

### <a name="official-specifications"></a>公式の仕様

* [USB 3.1 および USB タイプ-C 仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)
* [USB 電源配布](https://go.microsoft.com/fwlink/p/?LinkID=623310)

### <a name="applies-to"></a>適用対象

* Windows 10

### <a name="wdf-version"></a>WDF のバージョン

* KMDF バージョン1.15
* UMDF バージョン2.15

## <a name="important-apis"></a>重要な API

* [USB タイプ-C コネクタドライバープログラミングリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

USB タイプ C コネクタと、コネクタドライバーの予期される動作を管理する USB コネクタマネージャー (UCM) について説明します。

UCM は、WDF クラスの拡張クライアントドライバーモデルを使用して設計されています。 クラス拡張 (UcmCx) は、クライアントドライバーがコネクタに関する情報をレポートするために呼び出すことができるインターフェイスを提供する、Microsoft が提供する WDF ドライバーです。 UCM クライアントドライバーはコネクタのハードウェアインターフェイスを使用し、クラスの拡張機能はコネクタで発生するイベントを認識したままにします。 逆に、クラス拡張は、オペレーティングシステムイベントへの応答としてクライアントドライバーによって実装されるコールバック関数を呼び出します。

システムで USB タイプ C コネクタを有効にするには、クライアントドライバーを記述する必要があります。

![usb コネクタマネージャー](images/type-c-devnode.png)

## <a name="before-you-begin"></a>始める前に

* 開発用コンピューターに最新の Windows Driver Kit (WDK) を[インストール](https://go.microsoft.com/fwlink/p/?LinkID=623310)します。 キットには、UCM クライアントドライバーを作成するために必要なヘッダーファイルとライブラリが用意されています。具体的には、次のものが必要です。

  * スタブライブラリ (UcmCxstub .lib)。 ライブラリは、クライアントドライバーによって行われた呼び出しを変換し、UcmCx に渡します。
  * ヘッダーファイル (UcmCx)。

    ユーザーモードまたはカーネルモードで実行される UCM クライアントドライバーを作成できます。 ユーザーモードの場合は、UMDF 2.x ライブラリにバインドされます。カーネルモードの場合、KMDF 1.15 です。 プログラミングインターフェイスは、どちらのモードでも同じです。

    ![ucm の visual studio の構成](images/ucm-vs.png)

* クライアントドライバーが USB タイプ C コネクタと[Usb 電源配布](https://go.microsoft.com/fwlink/p/?LinkID=623310)の高度な機能をサポートするかどうかを決定します。

  このサポートにより、USB タイプ C コネクタ、USB タイプ C のドッキングとアクセサリ、および USB タイプ-C 充電器を使用して、Windows デバイスを構築することができます。 クライアントドライバーは、システムで USB および電力消費に関するポリシーを実装することをオペレーティングシステムに許可するコネクタイベントを報告します。

* Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) を、USB C コネクタを使用して、対象のコンピューターまたは Windows 10 Mobile にインストールします。
* UCM と他の Windows ドライバーとの相互作用について理解を深めます。 「[アーキテクチャ: Windows システム用の USB タイプ C 設計」を](architecture--usb-type-c-in-a-windows-system.md)参照してください。
* Windows Driver Foundation (WDF) について理解を深めます。 推奨される読み取り: 小額 Orwick および Guy Smith によって作成され[た Windows Driver Foundation を使用したドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)。

## <a name="summary-of-the-services-provided-by-the-ucm-class-extension"></a>UCM クラス拡張機能によって提供されるサービスの概要

UCM クラス拡張では、データと電源ロール、充電レベル、およびネゴシエートされた PD コントラクトの変更について、オペレーティングシステムに通知されます。 クライアントドライバーはハードウェアと対話しますが、変更が発生したときにクラスの拡張機能に通知する必要があります。 クラス拡張には、クライアントドライバーが通知を送信するために使用できる一連のメソッドが用意されています (このトピックで説明します)。 提供されるサービスを次に示します。

### <a name="data-role-configuration"></a>データロールの構成

USB タイプ C システムでは、データロール (ホストまたは機能) はコネクタの CC ピンの状態に依存します。 クライアントドライバーは、ポートが上流の接続ポート (UFP) に解決されたか、下流の接続ポート (UFP) に解決されているかを判断するために、ポートコントローラーから CC 行を読み取ります (「[アーキテクチャ: Windows システムの Windows システムの設計](architecture--usb-type-c-in-a-windows-system.md)」を参照してください)。 この情報をクラス拡張に報告し、現在のロールを USB ロールスイッチドライバーに報告できるようにします。

>[!NOTE]
> USB 役割スイッチドライバーは、Windows 10 Mobile システムで使用されます。 Windows 10 for desktop エディションのシステムでは、クラス拡張とロールスイッチドライバーの間の通信は任意です。 このようなシステムでは、デュアルロールコントローラーを使用しない場合があります。この場合、役割スイッチドライバーは使用されません。

### <a name="power-role-and-charging"></a>電源の役割と課金

クライアントドライバーは、USB タイプ C の現在の提供情報を読み取るか、またはパートナーコネクタを使用して PD 電源コントラクトをネゴシエートします。

* Windows 10 Mobile システムでは、適切なチャージャーを選択するかどうかはソフトウェアによって決まります。 クライアントドライバーは、課金レベルを充電アービトレーションドライバー (CAD .sys) に送信できるように、コントラクト情報をクラス拡張に報告します。 CAD は使用する現在のレベルを選択し、充電レベル情報をバッテリサブシステムに転送します。
* Windows 10 for desktop エディションのシステムでは、ハードウェアによって適切なチャージャーが選択されています。 クライアントドライバーは、その情報を取得し、クラス拡張に転送することを選択できます。 別の方法として、そのロジックを別のドライバーで実装することもできます。

### <a name="data-and-power-role-changes"></a>データと電源ロールの変更

PD 契約がネゴシエートされると、データロールとパワーロールが変更される可能性があります。 この変更は、クライアントドライバーまたはパートナーコネクタによって開始される場合があります。 クライアントドライバーは、その情報をクラス拡張に報告し、それに応じて再構成することができます。

### <a name="data-andor-power-role-update"></a>データやパワーロールの更新

オペレーティングシステムによって、現在のデータロールが正しくないと判断される場合があります。 その場合、クラス拡張は、必要なロールスワップ操作を実行するために、ドライバーのコールバック関数を呼び出します。

Microsoft 提供の USB タイプ C ポリシーマネージャーは、USB タイプ C コネクタのアクティビティを監視します。 Windows バージョン1809では、クライアントドライバーをポリシーマネージャーに書き込むために使用できる一連のプログラミングインターフェイスが導入されています。 クライアントドライバーは、USB タイプ C コネクタのポリシーの決定に参加できます。 このセットを使用して、カーネルモードのエクスポートドライバーまたはユーザーモードドライバーを作成できます。 詳細については、「 [USB タイプの書き込み-C ポリシーマネージャークライアントドライバー](policy-manager-client.md)」を参照してください。

## <a name="expected-behavior-of-the-client-driver"></a>クライアントドライバーの予期される動作

クライアントドライバーは、次のタスクを担当します。

* [CC] 行の変更を検出し、UFP、DFP などのパートナーの種類を決定します。 これを行うには、ドライバーは、USB タイプ C 仕様で定義されているように、完全なタイプ C のステートマシンを実装する必要があります。
* [CC] 行で検出された方向に基づいて Mux を構成します。 これには、PD トランスミッタ/レシーバーの有効化と、PD メッセージの処理と応答が含まれます。 これを行うには、ドライバーは、USB 電源配布2.0 仕様で定義されているように、完全な PD 受信機とトランスミッタのステートマシンを実装する必要があります。
* (ソースまたはシンクとしての) コントラクトの交渉、ロールの交換など、PD ポリシーの決定を行います。 クライアントドライバーは、最も適切なコントラクトを決定する役割を担います。
* 代替モードをアドバタイズしてネゴシエートし、別のモードが検出された場合は Mux を構成します。 クライアントドライバーは、ネゴシエートする代替モードを決定します。
* コネクタでの VBus/Vbus の制御。

## <a name="1-initialize-the-ucm-connector-object-ucmconnector"></a>1. UCM コネクタオブジェクトを初期化します (UCMCONNECTOR)

UCM connector オブジェクト (UCMCONNECTOR) は、USB タイプ C コネクタを表します。これは、UCM クラス拡張とクライアントドライバーの間の主なハンドルです。 オブジェクトは、コネクタの動作モードと電源供給機能を追跡します。

クライアントドライバーがコネクタの UCMCONNECTOR ハンドルを取得する順序の概要を次に示します。 次のタスクをドライバーの

1. [**UCM\_MANAGER\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/ns-ucmmanager-_ucm_manager_config)構造体への参照を渡すことによって、 [**UcmInitializeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucminitializedevice)を呼び出します。 ドライバーは、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出す前に、 [**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) callback 関数でこのメソッドを呼び出す必要があります。

2. [**UCM\_コネクタ\_TYPEC\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/ns-ucmmanager-_ucm_connector_typec_config)構造体の USB タイプ C コネクタの初期化パラメーターを指定します。 これには、コネクタの動作モードが含まれます。これには、ダウンストリーム接続ポートであるか、アップストリーム接続ポートであるか、またはデュアルロール対応であるかどうかが含まれます。 また、コネクタが電源に接続されている場合に、USB タイプ C の現在のレベルも指定します。 USB タイプ C コネクタは、3.5 mm オーディオジャックを操作できるように設計できます。 ハードウェアが機能をサポートしている場合は、コネクタオブジェクトをそれに応じて初期化する必要があります。

   構造体では、データロールを処理するために、クライアントドライバーのコールバック関数も登録する必要があります。

   このコールバック関数は、UCM クラス拡張によって呼び出されるコネクタオブジェクトに関連付けられています。 この関数は、クライアントドライバーによって実装される必要があります。

   [ *.EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)  
    パートナーコネクタにアタッチされている場合、コネクタのデータロールを指定されたロールにスワップします。

3. クライアントドライバーが PD 対応である場合、つまり、コネクタの電力配信2.0 ハードウェア実装を処理する場合は、PD を指定する[**UCM\_コネクタ\_pd\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/ns-ucmmanager-_ucm_connector_pd_config)構造体を初期化する必要もあります。初期化パラメーター。 これには、コネクタが電源シンクかソースかにかかわらず、電力フローが含まれます。

   また、クライアントドライバーのコールバック関数を登録して、電源ロールを処理する必要もあります。

   このコールバック関数は、UCM クラス拡張によって呼び出されるコネクタオブジェクトに関連付けられています。 この関数は、クライアントドライバーによって実装される必要があります。

   [ *.EVT\_UCM\_コネクタ\_\_POWER\_ロールの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)  
    パートナーコネクタに接続するときに、指定したロールにコネクタの電源ロールを設定します。

4. [**Ucmコネクター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorcreate)を呼び出し、コネクタの UCMCONNECTOR ハンドルを取得します。 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、クライアントドライバーがフレームワークデバイスオブジェクトを作成した後に、このメソッドを呼び出すようにしてください。 この呼び出しの適切な場所には、ドライバーの[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)または[**EVT_WDF_DEVICE_D0_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)を指定できます。

```cpp
EVT_UCM_CONNECTOR_SET_DATA_ROLE     EvtSetDataRole;

NTSTATUS
EvtDevicePrepareHardware(
    WDFDEVICE Device,
    WDFCMRESLIST ResourcesRaw,
    WDFCMRESLIST ResourcesTranslated
    )
{
    NTSTATUS status = STATUS_SUCCESS;
    PDEVICE_CONTEXT devCtx;
    UCM_MANAGER_CONFIG ucmCfg;
    UCM_CONNECTOR_CONFIG connCfg;
    UCM_CONNECTOR_TYPEC_CONFIG typeCConfig;
    UCM_CONNECTOR_PD_CONFIG pdConfig;
    WDF_OBJECT_ATTRIBUTES attr;
    PCONNECTOR_CONTEXT connCtx;

    UNREFERENCED_PARAMETER(ResourcesRaw);
    UNREFERENCED_PARAMETER(ResourcesTranslated);

    TRACE_FUNC_ENTRY();

    devCtx = GetDeviceContext(Device);

    if (devCtx->Connector)
    {
        goto Exit;
    }

    //
    // Initialize UCM Manager
    //
    UCM_MANAGER_CONFIG_INIT(&ucmCfg);

    status = UcmInitializeDevice(Device, &ucmCfg);
    if (!NT_SUCCESS(status))
    {
        TRACE_ERROR(
            "UcmInitializeDevice failed with %!STATUS!.",
            status);
        goto Exit;
    }

    TRACE_INFO("UcmInitializeDevice() succeeded.");

    //
    // Create a USB Type-C connector #0 with PD
    //
    UCM_CONNECTOR_CONFIG_INIT(&connCfg, 0);

    UCM_CONNECTOR_TYPEC_CONFIG_INIT(
        &typeCConfig,
        UcmTypeCOperatingModeDrp,
        UcmTypeCCurrentDefaultUsb | UcmTypeCCurrent1500mA | UcmTypeCCurrent3000mA);

    typeCConfig.EvtSetDataRole = EvtSetDataRole;

    UCM_CONNECTOR_PD_CONFIG_INIT(&pdConfig, UcmPowerRoleSink | UcmPowerRoleSource);

    connCfg.TypeCConfig = &typeCConfig;
    connCfg.PdConfig = &pdConfig;

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attr, CONNECTOR_CONTEXT);

    status = UcmConnectorCreate(Device, &connCfg, &attr, &devCtx->Connector);
    if (!NT_SUCCESS(status))
    {
        TRACE_ERROR(
            "UcmConnectorCreate failed with %!STATUS!.",
            status);
        goto Exit;
    }

    connCtx = GetConnectorContext(devCtx->Connector);

    UcmEventInitialize(&connCtx->EventSetDataRole);

    TRACE_INFO("UcmConnectorCreate() succeeded.");

Exit:

    TRACE_FUNC_EXIT();
    return status;
}
```

## <a name="2-report-the-partner-connector-attach-event"></a>2. パートナーコネクタのアタッチイベントを報告する

パートナーコネクタへの接続が検出された場合、クライアントドライバーは[**UcmConnectorTypeCAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)を呼び出す必要があります。 この呼び出しは、UCM クラス拡張に通知し、さらにオペレーティングシステムに通知します。 この時点で、システムは USB タイプ C レベルでの課金を開始する可能性があります。

UCM クラス拡張は、USB 役割スイッチドライバー (URS) にも通知します。 URS は、パートナーの種類に基づいて、ホストロールまたは機能ロールでコントローラーを構成します。 このメソッドを呼び出す前に、システム上の Mux が正しく構成されていることを確認してください。 そうしないと、システムが機能ロールにある場合は、正しくない速度 (SuperSpeed の代わりに高速) で接続されます。

```cpp
        UCM_CONNECTOR_TYPEC_ATTACH_PARAMS attachParams;

        UCM_CONNECTOR_TYPEC_ATTACH_PARAMS_INIT(
            &attachParams,
            UcmTypeCPortStateDfp);
        attachParams.CurrentAdvertisement = UcmTypeCCurrent1500mA;

        status = UcmConnectorTypeCAttach(
                    Connector,
                    &attachParams);
        if (!NT_SUCCESS(status))
        {
            TRACE_ERROR(
                "UcmConnectorTypeCAttach() failed with %!STATUS!.",
                status);
            goto Exit;
        }

        TRACE_INFO("UcmConnectorTypeCAttach() succeeded.");
```

## <a name="3-report-usb-type-c-advertisement-changes"></a>3. USB の種類-C の提供情報の変更を報告する

最初の attach イベントでは、partner コネクタは現在の提供情報を送信します。 パートナーが USB タイプのダウンストリーム接続ポートである場合に、提供情報がパートナーコネクタの現在のレベルを指定する場合。 それ以外の場合、提供情報は、UCMCONNECTOR ハンドル (ローカルコネクタ) によって表されるローカルコネクタの現在のレベルを指定します。 この初期提供情報は、接続の有効期間中に変更される可能性があります。 これらの変更は、クライアントドライバーによって監視される必要があります。

ローカルコネクタが電源シンクで、現在の提供情報が変更された場合、クライアントドライバーは現在の提供情報の変更を検出し、クラス拡張に報告する必要があります。 Windows 10 Mobile システムでは、この情報は、ソースからの現在の描画の量を調整するために、CAD およびバッテリサブシステムによって使用されます。 現在のレベルの変更をクラス拡張に報告するには、クライアントドライバーが[**UcmConnectorTypeCCurrentAdChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypeccurrentadchanged)を呼び出す必要があります。

## <a name="4-report-the-new-negotiated-pd-contract"></a>4. 新しいネゴシエートされた PD 契約を報告する

コネクタで PD がサポートされている場合、最初のアタッチイベントの後に、コネクタとそのパートナーコネクタ間で PD メッセージが転送されます。 両方のパートナーの間で、PD コントラクトがネゴシエートされます。これにより、コネクタで描画またはパートナーに描画を許可する現在のレベルが決まります。 PD コントラクトが変更されるたびに、クライアントドライバーはこれらのメソッドを呼び出して、変更をクラス拡張に報告する必要があります。

* クライアントドライバーは、パートナーからソース機能のアドバタイズ (要請されていない場合) を取得するときに、これらのメソッドを呼び出す必要があります。 ローカルコネクタ (シンク) は、パートナーがソースである場合にのみ、パートナーから要請されていない提供情報を取得します。 また、ローカルコネクタは、ソースとなることができるパートナーからのソース機能を明示的に要求できます (パートナーが現在シンクである場合でも)。 この交換は、 **Get\_Source\_cap**メッセージをパートナーに送信することによって行われます。
  * [**UcmConnectorPdPartnerSourceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdpartnersourcecaps)は、パートナーコネクタによってアドバタイズされるソース機能を報告します。
  * [**UcmConnectorPdConnectionStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)は、コントラクトの詳細を報告します。 このコントラクトは、要求データオブジェクトで説明されています。このオブジェクトは、Power Delivery 2.0 仕様で定義されています。
* 逆に、クライアントドライバーは、ローカルコネクタ (ソース) がパートナーにソース機能をアドバタイズするたびに、これらのメソッドを呼び出す必要があります。 また、ローカルコネクタは、パートナーから**Get\_source\_cap**メッセージを受信すると、ローカルコネクタのソース機能を使用して応答する必要があります。
  * [**UcmConnectorPdSourceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdsourcecaps)は、システムによってパートナーコネクタに提供されたソース機能を報告します。
  * [**UcmConnectorPdConnectionStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)は、現在ネゴシエートされている PD コントラクトの接続機能を報告します。

## <a name="5-report-battery-charging-status"></a>5. レポートバッテリの充電状態

課金レベルが適切でない場合、クライアントドライバーは UCM クラス拡張を通知できます。 クラス拡張は、この情報をオペレーティングシステムに報告します。 システムは、この情報を使用して、充電器がシステムを最適に充電できないことを示すユーザー通知を表示します。 課金の状態は、次の方法で報告できます。

* [**UcmConnectorChargingStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorchargingstatechanged)
* [**UcmConnectorTypeCAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)
* [**UcmConnectorPdConnectionStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)

これらのメソッドは、課金状態を指定します。 報告されるレベルが**UcmChargingStateSlowCharging**または**UcmChargingStateTrickleCharging** (「 [**UCM\_充電\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmtypes/ne-ucmtypes-_ucm_charging_state)」を参照) の場合、オペレーティングシステムはユーザー通知を表示します。

## <a name="6-report-pr_swapdr_swap-events"></a>6. PR\_スワップ/DR\_スワップイベントを報告する

コネクタがパートナーからの電源ロール (PR\_スワップ) またはデータロール (DR\_スワップ) のスワップメッセージを受信する場合、クライアントドライバーは UCM クラス拡張を通知する必要があります。

* [**Ucmコネクター Datadirection が変更されました**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)

  PD DR\_スワップメッセージが処理された後に、このメソッドを呼び出します。 この呼び出しの後、オペレーティングシステムは新しいロールを URS に報告します。これにより、既存のロールドライバーが破棄され、新しいロールのドライバーが読み込まれます。

* [**Ucmコネクター Powerdirection が変更されました**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)

  このメソッドは、PD PR\_スワップメッセージが処理された後に呼び出されます。 PR\_スワップした後、PD コントラクトを再ネゴシエートする必要があります。 クライアントドライバーは、[手順 4](#4-report-the-new-negotiated-pd-contract). で説明されているメソッドを呼び出すことによって、PD コントラクトネゴシエーションを報告する必要があります。

## <a name="7-implement-callback-functions-to-handle-power-and-data-role-swap-requests"></a>7. コールバック関数を実装して、パワーおよびデータロールのスワップ要求を処理する

UCM クラス拡張は、コネクタのデータまたは電源の方向を変更する要求を受け取る場合があります。 このような場合は、クライアントドライバーの[ *.evt\_UCM\_コネクタの実装を呼び出し\_\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)と[ *.evt\_UCM\_コネクタ\_設定\_電源\_の役割*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)を設定します。コールバック関数 (コネクタが PD を実装している場合)。 クライアントドライバーは、 [**Ucmコネクター作成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorcreate)の呼び出しでこれらの関数を以前に登録しました。

クライアントドライバーは、ハードウェアインターフェイスを使用して、ロールスワップ操作を実行します。

* [ *.EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)

  コールバック実装では、クライアントドライバーは次のことを想定しています。

  1. PD DR\_スワップメッセージをポートパートナーに送信します。
  2. [**Ucmコネクター Datadirection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)を呼び出して、メッセージシーケンスが正常に完了したか失敗したかをクラスの拡張に通知します。

    ```cpp
    EVT_UCM_CONNECTOR_SET_DATA_ROLE     EvtSetDataRole;  

    NTSTATUS  
    EvtSetDataRole(  
        UCMCONNECTOR  Connector,  
        UCM_TYPE_C_PORT_STATE DataRole  
        )  
    {  
        PCONNECTOR_CONTEXT connCtx;  

        TRACE_INFO("EvtSetDataRole(%!UCM_TYPE_C_PORT_STATE!) Entry", DataRole);  

        connCtx = GetConnectorContext(Connector);

        TRACE_FUNC_EXIT();  

        return STATUS_SUCCESS;  
    }  
    ```

* [ *.EVT\_UCM\_コネクタ\_\_POWER\_ロールの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)

    コールバック実装では、クライアントドライバーは次のことを想定しています。

  1. PD PR\_スワップメッセージをポートパートナーに送信します。
  2. [**Ucmコネクター Powerdirection が変更さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)れ、メッセージシーケンスが正常に完了したか失敗したかをクラスの拡張に通知するようになりました。

    ```cpp
    EVT_UCM_CONNECTOR_SET_POWER_ROLE     EvtSetPowerRole;  

    NTSTATUS  
    EvtSetPowerRole(  
        UCMCONNECTOR Connector,  
        UCM_POWER_ROLE PowerRole  
        )  
    {  
        PCONNECTOR_CONTEXT connCtx;  

        TRACE_INFO("EvtSetPowerRole(%!UCM_POWER_ROLE!) Entry", PowerRole);  

        connCtx = GetConnectorContext(Connector);  

        //PR_Swap operation.  

        TRACE_FUNC_EXIT();  

        return STATUS_SUCCESS;  
    }  
    ```

>[!NOTE]
>クライアントドライバーは、 [**Ucmコネクター Datadirection changed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)および[**Ucmコネクター powerdirection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)を非同期的に呼び出すことができます。これは、コールバックスレッドからの変更ではありません。 一般的な実装では、クラス拡張はコールバック関数を呼び出します。これにより、クライアントドライバーは、メッセージを送信するハードウェアトランザクションを開始します。 トランザクションが完了すると、ハードウェアからドライバーに通知されます。 ドライバーは、これらのメソッドを呼び出して、クラスの拡張を通知します。

## <a name="8-report-the-partner-connector-detach-event"></a>8. パートナーコネクタのデタッチイベントを報告する

パートナーコネクタへの接続が終了すると、クライアントドライバーは[**UcmConnectorTypeCDetach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecdetach)を呼び出す必要があります。 この呼び出しは、UCM クラス拡張に通知し、さらにオペレーティングシステムに通知します。

## <a name="use-case-example-mobile-device-connected-to-a-pc"></a>ユースケース例: PC に接続されているモバイルデバイス

Windows 10 Mobile を実行しているデバイスが、USB タイプ C 接続経由で Windows 10 for desktop エディションを実行している PC に接続されている場合、MTP はその方向でのみ機能するため、オペレーティングシステムによって、モバイルデバイスがアップストリームのポート (UFP) であることが確認されます。 このシナリオでは、データロールの修正の順序は次のようになります。

1. モバイルデバイスで実行されているクライアントドライバーは、 [**UcmConnectorTypeCAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)を呼び出してアタッチイベントを報告し、ダウンストリームの接続ポート (ufp) としてパートナーコネクタを報告します。
2. クライアントドライバーは、 [**UcmConnectorPdPartnerSourceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdpartnersourcecaps)および[**UcmConnectorPdConnectionStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)を呼び出すことによって、PD コントラクトを報告します。
3. UCM クラス拡張は、これらのドライバーがホストからの列挙に応答する原因となった USB デバイス側ドライバーに通知します。 オペレーティングシステムの情報は、USB を介して交換されます。
4. UCM クラス拡張 UcmCx は、クライアントドライバーのコールバック関数を呼び出して、 [ *\_DATA\_ROLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)および[ *.evt\_UCM\_CONNECTOR\_set\_設定して\_コネクタを変更し\_ます。電源\_役割*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)。

>[!NOTE]
>2つの Windows 10 Mobile デバイスが互いに接続されている場合、役割のスワップは実行されず、接続が有効な接続ではないことがユーザーに通知されます。

## <a name="related-topics"></a>関連トピック

[USB Type-C コネクタ用 Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)  
