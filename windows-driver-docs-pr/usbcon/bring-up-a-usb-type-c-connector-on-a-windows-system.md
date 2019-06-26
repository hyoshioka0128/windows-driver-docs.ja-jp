---
Description: USB タイプ-c コネクタとコネクタのドライバーの想定される動作を管理する USB コネクタ マネージャ (UCM) について説明します。
title: USB Type-C コネクタ ドライバーを記述する
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: ae332af09dd9941e24f1415ff97b3b106d895151
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384484"
---
# <a name="write-a-usb-type-c-connector-driver"></a>USB Type-C コネクタ ドライバーを記述する

これらのシナリオで USB 型-c コネクタのドライバーを記述する必要があります。

* USB タイプ-c ハードウェアに電源 (PD) の配信のステート マシンを処理する機能がある場合。 それ以外の場合、型-C# の USB ポート コント ローラーのドライバーを書き込むことを検討します。 詳細については、次を参照してください。[型-C# の USB ポート コント ローラー ドライバー](write-a-usb-type-c-port-controller-driver.md)します。

* 場合は、ハードウェアの埋め込みコント ローラーではありません。 それ以外の場合、Microsoft によって提供されるインボックス ドライバー、UcmUcsi.sys を読み込みます。 (を参照してください[UCSI ドライバー](ucsi.md)) ACPI トランスポートまたは[UCSI クライアント ドライバーを書く](write-a-ucsi-driver.md)非 ACPI トランスポート。

## <a name="summary"></a>概要

* クラスの拡張機能とクライアント ドライバーによって使用される UCM オブジェクト
* UCM クラスの拡張機能によって提供されるサービス
* クライアント ドライバーの想定される動作

### <a name="official-specifications"></a>公式の仕様

* [USB 3.1 と USB 型-C# の仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)
* [USB 電源配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)

### <a name="applies-to"></a>対象

* Windows 10

### <a name="wdf-version"></a>WDF のバージョン

* KMDF バージョン 1.15
* UMDF 2.15 バージョン

## <a name="important-apis"></a>重要な API

* [USB タイプ-c コネクタ ドライバーのプログラミング リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

USB タイプ-c コネクタとコネクタのドライバーの想定される動作を管理する USB コネクタ マネージャ (UCM) について説明します。

UCM は WDF クラスの拡張機能クライアント ドライバー モデルを使用して設計されています。 クラスの拡張機能 (UcmCx) は、コネクタに関する情報を報告するクライアント ドライバーを呼び出すことができるインターフェイスを提供する Microsoft 提供の WDF ドライバーです。 UCM クライアント ドライバーでは、コネクタのハードウェア インターフェイスを使用し、コネクタで発生するイベントの認識クラスの拡張機能を保持します。 逆に、クラス拡張は、オペレーティング システムのイベントへの応答でクライアント ドライバーによって実装されるコールバック関数を呼び出します。

システム上の C-USB 型コネクタを有効にするには、クライアント ドライバーを記述する必要があります。

![usb コネクタ マネージャー](images/type-c-devnode.png)

## <a name="before-you-begin"></a>始める前に

* [インストール](https://go.microsoft.com/fwlink/p/?LinkID=623310)開発用コンピューターに最新 Windows Driver Kit (WDK)。 このキットが必要なヘッダー ファイルと具体的には、UCM クライアント ドライバーを記述するためのライブラリ、する必要があります。

  * スタブ ライブラリは、(UcmCxstub.lib)。 ライブラリは、クライアント ドライバーによって行われた呼び出しを変換し、UcmCx まで渡したりします。
  * ヘッダー ファイルでは、UcmCx.h します。

    ユーザー モードまたはカーネル モードで実行されている UCM クライアント ドライバーを作成することができます。 ユーザー モードの場合、UMDF 2.x ライブラリとバインドします。カーネル モード KMDF 1.15 です。 プログラミング インターフェイスは、どちらのモードと同じです。

    ![ucm の visual studio の構成](images/ucm-vs.png)

* クライアント ドライバーが USB 型-c コネクタの高度な機能をサポートするかどうかを決定し、 [USB 電力配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)します。

  このサポートでは、USB 型-c コネクタ、USB 型-C# のドッキングし、[アクセサリ]、USB 型-C# の充電器と Windows デバイスを作成することができます。 クライアント ドライバーでは、オペレーティング システムの USB に関するポリシーを実装し、システムの電源を消費できるようにコネクタ イベントを報告します。

* ターゲット コンピューターまたは Windows 10 Mobile にデスクトップのエディション (Home、Pro、Enterprise、および Education) が型-C# の USB コネクタの使用には、Windows 10 をインストールします。
* UCM およびその他の Windows ドライバーと対話する方法を理解します。 参照してください[アーキテクチャ。Windows システムの USB 型-C# のデザイン](architecture--usb-type-c-in-a-windows-system.md)します。
* Windows Driver Foundation (WDF) を理解します。 参考資料。[Windows Driver Foundation でのドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)少額 Orwick と Guy Smith によって書き込まれた、します。

## <a name="summary-of-the-services-provided-by-the-ucm-class-extension"></a>UCM クラスの拡張機能が提供するサービスの概要

UCM クラスの拡張機能は、データと電源のロール、充電レベル、およびネゴシエートされた PD コントラクトの変更に関する情報を通知するオペレーティング システムを保持します。 クライアント ドライバーは、ハードウェアと対話する、中に、これらの変更が発生した場合、クラスの拡張機能を通知する必要があります。 クラスの拡張機能では、クライアント ドライバーは、(このトピックで説明) 通知の送信に使用できるメソッドのセットを提供します。 提供されるサービスを次に示します。

### <a name="data-role-configuration"></a>データ ロールの構成

USB 型-C# のシステムでは、データの役割 (ホストまたは関数) は、コネクタの [cc] ピンの状態によって異なります。 クライアント ドライバーは、[cc] 行を読み取ります (を参照してください[アーキテクチャ。Windows システムの USB 型-C# のデザイン](architecture--usb-type-c-in-a-windows-system.md)) ポートがアップ ストリームに接続するポート (UFP) またはダウン ストリームに接続するポート (UFP) に解決されているかどうかを判断する、ポートのコント ローラーからの状態。 役割の交代の USB ドライバーを現在のロールを報告できるように、クラスの拡張機能には、その情報を報告します。

>[!NOTE]
> Windows 10 Mobile のシステムの役割の交代の USB ドライバーが使用されます。 Windows 10 デスクトップ エディションのシステムでは、クラスの拡張機能と役割の交代ドライバー間の通信は省略可能です。 このようなシステムがありますいないデュアル ロール コント ローラーを使用、する場合は、役割の交代ドライバーは使用されません。

### <a name="power-role-and-charging"></a>電源の役割と課金

クライアント ドライバーでは、USB 型-c 現在提供情報を読み取るか、PD power コントラクト パートナー コネクタの使用をネゴシエートします。

* Windows 10 Mobile のシステムでは、適切な充電器を選択するかどうかはソフトウェア支援型です。 充電レベル、充電調停ドライバー (CAD.sys) に送信できるように、クライアント ドライバーは、クラスの拡張にコントラクト情報を報告します。 CAD は、使用する現在のレベルを選択し、サブシステムにバッテリ充電レベルの情報を転送します。
* システムのデスクトップ エディションの Windows 10 では、適切な充電器は、ハードウェアで選択されます。 クライアント ドライバーは、その情報を取得し、クラスの拡張に転送できます。 または、別のドライバーがそのロジックを実装することがあります。

### <a name="data-and-power-role-changes"></a>データと出力のロール変更

PD コントラクトをネゴシエートするとデータ ロールと電源のロールが変更可能性があります。 その変更は、クライアントは、ドライバーまたはパートナー コネクタによって開始可能性があります。 クライアント ドライバーは、それに応じて処理を構成こと可能性があります再ようにするために、クラスの拡張機能には、その情報を報告します。

### <a name="data-andor-power-role-update"></a>データや電源ロールの更新

オペレーティング システムは、現在のデータ ロールが正しくないことにあります。 その場合は、クラス拡張は、必要なロールのスワップ操作を実行するドライバーのコールバック関数を呼び出します。

Microsoft から提供された USB 型 C ポリシー マネージャーは、USB 型-C# のコネクタのアクティビティを監視します。 Windows、バージョンは 1809 には、一連のポリシー マネージャーにクライアント ドライバーを記述するインターフェイスのプログラミングが導入されています。 クライアント ドライバーは、USB 型-C# のコネクタのポリシーの決定に参加できます。 この設定すると、エクスポート カーネル モード ドライバーまたはユーザー モード ドライバーを記述できます。 詳細については、次を参照してください。[種類 C ポリシー マネージャーの USB クライアント ドライバーの記述](policy-manager-client.md)します。

## <a name="expected-behavior-of-the-client-driver"></a>クライアント ドライバーの想定される動作

クライアント ドライバーでは、これらのタスクを担います。

* [Cc] 行に変更を検出し、UFP、DFP、およびその他のユーザーなどのパートナーの種類を決定します。 これを行うには、完全に、ドライバーは実装する必要があります型 C ステート マシン型-C# の USB 仕様で定義されています。
* [Cc] 行で検出された方向に基づき、Mux を構成します。 これには、処理および PD メッセージに応答して PD トランスミッタ/レシーバーの有効化が含まれます。 これを行うには、ドライバーは、完全な PD 受信者および送信者状態マシン USB 電力配信 2.0 仕様で定義されているを実装する必要があります。
* (ソースまたはシンク) としてのコントラクト、ロールの交換、およびその他のネゴシエーションなど、PD ポリシーの決定を行います。 クライアント ドライバーが、最も適切なコントラクトを判断します。
* アドバタイズし代替のモードをネゴシエートし、別のモードが検出された場合に、Mux を構成します。 クライアント ドライバーでは、ネゴシエートする代替のモードを決定します。
* コネクタを介して VBus/VConn のコントロールです。

## <a name="1-initialize-the-ucm-connector-object-ucmconnector"></a>1. UCM コネクタ オブジェクト (UCMCONNECTOR) の初期化します。

UCM コネクタ オブジェクト (UCMCONNECTOR) は、C-USB 型コネクタを表し、UCM クラスの拡張機能と、クライアント ドライバーとの間の主要なハンドルです。 オブジェクトは、コネクタの動作モードと機能をソーシングの電源を追跡します。

クライアント ドライバーが、コネクタの UCMCONNECTOR ハンドルを取得するシーケンスの概要を次に示します。 これらのタスクをドライバーの実行します。

1. 呼び出す[ **UcmInitializeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucminitializedevice)への参照を渡すことによって、 [ **UCM\_MANAGER\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/ns-ucmmanager-_ucm_manager_config)構造体。 ドライバーこのメソッドを呼び出す必要があります、 [ **EVT_WDF_DRIVER_DEVICE_ADD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)呼び出す前に、コールバック関数[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

2. USB タイプ-c のコネクタの初期化パラメーターを指定、 [ **UCM\_コネクタ\_種類が「\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/ns-ucmmanager-_ucm_connector_typec_config)構造体。 これは、ダウン ストリームに接続するポート、アップ ストリームに接続するポート、またはデュアル ロールかどうかに、コネクタの動作モードが含まれます対応します。 また、コネクタは、電源と USB 型-C# の現在のレベルを指定します。 USB タイプ-c コネクタは、3.5 mm のオーディオ ジャックを操作できるように設計できます。 ハードウェアの機能をサポートする場合コネクタ オブジェクトをそれに応じて初期化する必要があります。

   構造体で、ロールのデータを処理するためのクライアント ドライバーのコールバック関数を登録することも必要があります。

   このコールバック関数は、UCM クラスの拡張機能によって呼び出されるコネクタ オブジェクトに関連付けられます。 クライアント ドライバーでは、この関数を実装する必要があります。

   [*EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)  
    データのパートナー コネクタに接続すると、指定したロールへのコネクタの役割を交換します。

3. PD 対応している場合、クライアント ドライバーは、コネクタの Power 配信 2.0 ハードウェアの実装には、処理、初期化することも必要があります、 [ **UCM\_コネクタ\_PD\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/ns-ucmmanager-_ucm_connector_pd_config) PD 初期化パラメーターを指定する構造体。 コネクタは、電源シンクまたはソースかどうか、power のフローが含まれます。

   構造体で、電源の役割を処理するためのクライアント ドライバーのコールバック関数を登録することも必要があります。

   このコールバック関数は、UCM クラスの拡張機能によって呼び出されるコネクタ オブジェクトに関連付けられます。 クライアント ドライバーでは、この関数を実装する必要があります。

   [*EVT\_UCM\_コネクタ\_設定\_POWER\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)  
    パートナー コネクタに接続されているときに指定されたロールには、コネクタの power ロールを設定します。

4. 呼び出す[ **UcmConnectorCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorcreate)およびコネクタの UCMCONNECTOR ハンドルを取得します。 クライアント ドライバーが呼び出すことによって、framework デバイス オブジェクトを作成後に、このメソッドを呼び出すかどうかを確認[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。 この呼び出しの適切な場所は、ドライバーにできる[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)または[ **EVT_WDF_DEVICE_D0_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)します。

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

## <a name="2-report-the-partner-connector-attach-event"></a>2. レポートのパートナー コネクタ イベントをアタッチします。

クライアント ドライバーを呼び出す必要があります[ **UcmConnectorTypeCAttach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)パートナー コネクタへの接続が検出されたとき。 この呼び出しは、さらに、オペレーティング システムに通知 UCM クラスの拡張を通知します。 この時点で、システムが USB 型-C# のレベルで課金を起動することがあります。

UCM クラスの拡張機能は、役割の交代の USB ドライバー (URS) にも通知します。 URS は、パートナーの種類に基づいて、ホストの役割または役割が関数で、コント ローラーを構成します。 このメソッドを呼び出す前に、システムに Mux が正しく構成されていることを確認します。 それ以外の場合、関数の役割が、システムにある場合、不適切な速度 (SuperSpeed ではなく高速) で接続します。

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

## <a name="3-report-usb-type-c-advertisement-changes"></a>3.USB タイプ-c 提供情報の変更を報告

最初にアタッチ イベント、パートナーのコネクタが現在の提供情報を送信します。 場合は、提供情報は、パートナーが USB 型から C のダウン ストリームに接続するポートにパートナー コネクタの現在のレベルを指定します。 それ以外の場合、提供情報には、UCMCONNECTOR ハンドル (ローカル コネクタ) で表される、ローカル コネクタの現在のレベルを指定します。 この初期の提供情報は、接続の有効期間中に変更可能性があります。 クライアント ドライバーでは、これらの変更を監視する必要があります。

ローカル コネクタが電源シンクと現在の提供情報の変更の場合は、クライアント ドライバーが現在の提供情報の変更を検出し、クラスの拡張機能に報告する必要があります。 Windows 10 Mobile のシステムでは、その情報は現在のソースから描画の量を調整する CAD.sys してバッテリ サブシステムに使用されます。 現在のレベルの変更をクラスの拡張機能を報告するクライアント ドライバーを呼び出す必要があります[ **UcmConnectorTypeCCurrentAdChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectortypeccurrentadchanged)します。

## <a name="4-report-the-new-negotiated-pd-contract"></a>4。レポートの新しいネゴシエート PD コントラクト

コネクタは、最初のイベントをアタッチした後、PD をサポートする場合、コネクタとそのパートナー コネクタ間で転送される PD メッセージがあります。 両方のパートナーとの間、現在、コネクタが描画または描画するためにパートナーを許可することができますのレベルを決定する PD コントラクトがネゴシエートされます。 毎回 PD 契約の変更、クライアント ドライバー呼び出す必要があります、クラスの拡張機能に変更を報告するこれらのメソッド。

* クライアント ドライバーは、ソース機能提供情報 (要請されていない、またはそれ以外の場合)、パートナーから取得されるたびに、これらのメソッドを呼び出す必要があります。 ローカル コネクタ (シンク) は、パートナーが、ソースである場合にのみ、パートナーから要請されていない提供情報を取得します。 また、ローカルのコネクタが (現在は、パートナーは、シンク) の場合でも、ソースの対応しているパートナーからソースの機能を明示的に要求することができます。 交換が送信することで、**取得\_ソース\_Cap**パートナーにメッセージ。
  * [**UcmConnectorPdPartnerSourceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdpartnersourcecaps)パートナー コネクタによってアドバタイズされたソースの機能を報告します。
  * [**UcmConnectorPdConnectionStateChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)コントラクトの詳細をレポートします。 コントラクトは、要求のデータ オブジェクト、電力配信 2.0 仕様で定義されている説明します。
* 逆に、クライアント ドライバー呼び出す必要がありますこれらのメソッドごとに、ローカル コネクタ (ソース) は、パートナーにソース機能をアドバタイズします。 また、ローカル コネクタを受け取るときに、**を取得\_ソース\_Cap**メッセージ ローカル コネクタのソースの機能を備えた、パートナーから応答する必要があります。
  * [**UcmConnectorPdSourceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdsourcecaps)パートナー コネクタに、システムによって提供されたソースの機能を報告します。
  * [**UcmConnectorPdConnectionStateChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged) PD コントラクトをネゴシエートされた現在の接続機能をレポートします。

## <a name="5-report-battery-charging-status"></a>5。レポートのバッテリ充電状態

充電レベルが十分でない場合、クライアント ドライバーでは、UCM クラスの拡張機能を通知できます。 クラスの拡張機能では、オペレーティング システムには、この情報を報告します。 システムでは、その情報を使用して、ユーザー通知を表示する充電器によってシステムが最適に充電されないようにします。 これらのメソッドによって充電状態を報告できます。

* [**UcmConnectorChargingStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorchargingstatechanged)
* [**UcmConnectorTypeCAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)
* [**UcmConnectorPdConnectionStateChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged)

これらのメソッドは、充電状態を指定します。 報告されたレベルの場合**UcmChargingStateSlowCharging**または**UcmChargingStateTrickleCharging** (を参照してください[ **UCM\_充電中\_状態** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtypes/ne-ucmtypes-_ucm_charging_state))、オペレーティング システムは、ユーザー通知を示しています。

## <a name="6-report-prswapdrswap-events"></a>6。レポートの PR\_スワップ/DR\_スワップ イベント

コネクタは、電源のロールを受信した場合 (PR\_スワップ) またはデータ ロール (DR\_スワップ) クライアント ドライバーは、UCM クラスの拡張機能を通知する必要があります、パートナーからメッセージを交換します。

* [**UcmConnectorDataDirectionChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)

  PD DR 後にこのメソッドを呼び出す\_スワップ メッセージが処理されています。 この呼び出しの後は、オペレーティング システムは、URS、既存のロールのドライバーを廃棄し、新しいロールのドライバーをロードする、新しいロールを報告します。

* [**UcmConnectorPowerDirectionChanged**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)

  PD PR の後にこのメソッドを呼び出し\_スワップ メッセージが処理されています。 プル要求の後に\_スワップ、PD コントラクトが再ネゴシエートする必要があります。 クライアント ドライバーで説明されているメソッドを呼び出して、その PD 契約交渉を報告する必要があります[手順 4](#4-report-the-new-negotiated-pd-contract)します。

## <a name="7-implement-callback-functions-to-handle-power-and-data-role-swap-requests"></a>7.電源とデータ ロールの交替申請を処理するコールバック関数を実装

UCM クラスの拡張機能は、コネクタのデータまたは電源の方向を変更する要求を取得する可能性があります。 その場合は、クライアント ドライバーの実装を呼び出す[ *EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)と[*EVT\_UCM\_コネクタ\_設定\_POWER\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)コールバック関数 (実装している場合、コネクタ PD)。 クライアント ドライバーがこれらの関数を呼び出しで既に登録[ **UcmConnectorCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorcreate)します。

クライアント ドライバーでは、ハードウェアのインターフェイスを使用してロールのスワップ操作を実行します。

* [*EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)

  コールバックの実装では、クライアント ドライバーに期待されます。

  1. 送信 PD DR\_ポート パートナーにメッセージをスワップします。
  2. 呼び出す[ **UcmConnectorDataDirectionChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)に成功したか、メッセージ シーケンスが完了したクラスの拡張を通知します。

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

* [*EVT\_UCM\_コネクタ\_設定\_POWER\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)

    コールバックの実装では、クライアント ドライバーに期待されます。

  1. PD PR を送信\_ポート パートナーにメッセージをスワップします。
  2. 呼び出す[ **UcmConnectorPowerDirectionChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)に成功したか、メッセージ シーケンスが完了したクラスの拡張を通知します。

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
>クライアント ドライバーが呼び出せる[ **UcmConnectorDataDirectionChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectordatadirectionchanged)と[ **UcmConnectorPowerDirectionChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpowerdirectionchanged)非同期的に、コールバック スレッドはありません。 一般的な実装では、クラスの拡張機能は、メッセージを送信するハードウェアのトランザクションを開始するクライアント ドライバーが発生したコールバック関数を呼び出します。 トランザクションが完了したら、ハードウェアには、ドライバーに通知します。 ドライバーは、クラスの拡張機能を通知するこれらのメソッドを呼び出します。

## <a name="8-report-the-partner-connector-detach-event"></a>8.レポートのパートナー コネクタ イベントをデタッチします。

クライアント ドライバーを呼び出す必要があります[ **UcmConnectorTypeCDetach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectortypecdetach)パートナー コネクタへの接続が終了します。 この呼び出しは、さらに、オペレーティング システムに通知 UCM クラスの拡張を通知します。

## <a name="use-case-example-mobile-device-connected-to-a-pc"></a>ケースの例を使用します。PC に接続されているモバイル デバイス

型から C の USB 接続経由でデスクトップ エディションの Windows 10 を実行している PC に Windows 10 Mobile を実行しているデバイスが接続されると、オペレーティング システムにより MTP がその方向でのみ機能するため、そのモバイル デバイスがアップ ストリームに接続するポート (UFP) を確認します。 このシナリオでデータ ロールの修正の順序を次に示します。

1. モバイル デバイスで実行されているクライアント ドライバーは、呼び出すことによって添付イベントを報告する[ **UcmConnectorTypeCAttach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectortypecattach)およびパートナー コネクタとして、ダウン ストリームに接続するポート (UFP) をレポートします。
2. クライアント ドライバーは、呼び出すことによって PD コントラクトを報告[ **UcmConnectorPdPartnerSourceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdpartnersourcecaps)と[ **UcmConnectorPdConnectionStateChanged** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nf-ucmmanager-ucmconnectorpdconnectionstatechanged).
3. UCM クラスの拡張機能では、USB デバイス側ドライバーが原因で、ホストから列挙型に対応するそれらのドライバーに通知します。 オペレーティング システムの情報は、USB 経由で交換されます。
4. UcmCx UCM クラスの拡張は、ロールを変更する、クライアント ドライバーのコールバック関数を呼び出します。[*EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)と[ *EVT\_UCM\_コネクタ\_設定\_POWER\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)します。

>[!NOTE]
>2 つの Windows 10 Mobile デバイスは相互に接続されている、役割の交代には実行されず、し、接続が有効な接続ではないユーザーに通知されます。

## <a name="related-topics"></a>関連トピック

[USB Type-C コネクタ用 Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)  
