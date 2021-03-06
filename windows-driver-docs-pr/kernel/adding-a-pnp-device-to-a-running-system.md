---
title: 実行中システムへの PnP デバイスの追加
description: 実行中システムへの PnP デバイスの追加
ms.assetid: 73d14ba1-6cf1-44eb-8a98-8c2fe44c11bb
keywords:
- PnP WDK カーネルでは、システムを実行しているデバイスを追加します。
- プラグ アンド プレイ WDK カーネル、システムを実行しているデバイスを追加します。
- システムを実行している PnP デバイスの追加
- PnP デバイス PnP WDK の列挙
- PnP デバイスの報告
- devnode PnP WDK
- デバイス ノード PnP WDK
- 機能ドライバー WDK PnP
- フィルター ドライバー WDK PnP
- AddDevice ルーチン PnP WDK
- WDK PnP Irp
- I/O 要求パケット PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc9ae4fe91b5ccd2b10496c5e367bfee0376cecc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369996"
---
# <a name="adding-a-pnp-device-to-a-running-system"></a>実行中システムへの PnP デバイスの追加





このセクションでは、システムは、ユーザーが実行中のマシンに追加する PnP デバイスを構成するときに発生するイベントのシーケンスについて説明します。 この説明には、PnP マネージャー、バス ドライバー、およびを列挙して、新しいデバイスを構成する関数とフィルター ドライバーのロールが強調表示されます。

この説明のほとんどは、マシンが起動したときに存在する PnP デバイスの構成に関連するもあります。 具体的には、デバイスがドライバーには、サービスがマークされているが\_デマンド\_デバイスが動的に追加またはがブート時に存在するかどうか、INF ファイルで開始が基本的に同じ方法で構成されます。

次の図は、ユーザー、コンピューターにハードウェアを接続するときから、デバイスの構成で、最初の手順を示します。

![列挙とプラグ アンド プレイ デバイスのレポートを示す図します。](images/hotplug.png)

次のノートは、前の図の丸の番号に対応しています。

1.  ユーザーは、PnP バス上の空きスロットに PnP デバイスを接続します。

    この例では、ユーザーは、PnP USB ジョイスティックを USB ホスト コント ローラーでハブに接続します。 USB ハブは、子デバイスを接続しているために、バスの PnP デバイスです。

2.  新しいデバイスが、バスがある関数のドライバー、バスのデバイスを決定します。

    ドライバーがこれを決定する方法は、バス アーキテクチャによって異なります。 いくつかのバスは、バス関数ドライバーは、新しいデバイスのホット プラグ通知を受け取ります。 バスがホット プラグ通知をサポートしていない場合、ユーザーを列挙するバスのコントロール パネルで適切な処置を実行する必要があります。

    この例では、USB バスは、その子が変更されている関数のドライバーを USB バスが通知されるようにホットプラグ通知をサポートします。

3.  バス デバイスの機能のドライバーは、一連の子デバイスが変更されたことを PnP マネージャーに通知します。

    関数のドライバーを呼び出して PnP マネージャーに通知[ **IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)で、*型*の**BusRelations**します。

4.  PnP マネージャーでは、バス上のデバイスの現在の一覧については、バスのドライバーを照会します。

    PnP マネージャーに送信、 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)バスのデバイス スタックを要求します。 **Parameters.QueryDeviceRelations.Type**値は**BusRelations**、バス上に存在するデバイスの現在の一覧については、PnP マネージャーが確認することを示します (*バス関係*).

    PnP マネージャーでは、バスのデバイス スタックの最上位のドライバーを IRP を送信します。 PnP Irp の規則に従っては、スタック内の各ドライバーは、必要に応じて、IRP を処理し、次のドライバーに IRP を渡します。

5.  関数のドライバー、バスのデバイスを IRP を処理します。

    リファレンス ページを参照してください。 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)この IRP の処理の詳細について。

    この例では、USB ハブのドライバーを処理のハブには、この IRP *FDO*します。 ハブのドライバーを作成、 *PDO*ジョイスティック デバイスの IRP に返される子デバイスの一覧に含めず、ジョイスティック PDO への参照先のポインターが含まれています。

    IRP のいずれかを使用してバックアップ デバイス スタックを移動、USB ハブの親バス ドライバー (USB ホスト コント ローラー クラス/miniclass ドライバー ペア) には、IRP が完了すると、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)登録されたルーチンハブのドライバーです。

バス関数のドライバーが要求 PnP マネージャーが子デバイスの一覧のクエリを実行して子の一覧の変更を報告することに注意してください。 結果の**IRP\_MN\_クエリ\_デバイス\_リレーション**bus デバイスのすべてのドライバーが要求を表示します。 通常、バス関数ドライバーは IRP とレポートの子を処理するためにのみ、ドライバーです。 一部のデバイス スタックでは、bus フィルター ドライバーが存在し、バス関係のリストの作成に参加しています。 1 つの例は、ACPI で、デバイスを ACPI bus フィルター ドライバーとしてアタッチします。 一部のデバイス スタックで nonbus フィルター ドライバーの処理、 **IRP\_MN\_クエリ\_デバイス\_リレーション**要求が、これは一般的ではありません。

この時点では、PnP マネージャーは、バス上のデバイスの現行一覧が。 PnP マネージャーには、すべてのデバイスは、新しく到着したか、削除されているかどうかを決定します。 この例では、1 つの新しいデバイスです。 次の図は、新しいデバイスの devnode を作成して、デバイスの構成を開始、PnP マネージャーを示します。

![新しいプラグ アンド プレイ デバイスの devnode を作成するかを示す図](images/credvnd.png)

次のノートは、前の図の丸の番号に対応しています。

1.  PnP マネージャー devnode を作成、新しい子のデバイス、バスにします。

    PnP マネージャーで返される bus 関係の一覧を比較し、 **IRP\_MN\_クエリ\_デバイス\_リレーション**IRP のバスの子の一覧には現在、PnP で記録デバイス ツリー。 PnP マネージャーでは、新しい各デバイスの devnode を作成し、削除されたすべてのデバイスの削除処理を開始します。

    この例では、1 つの新しいデバイス (ジョイスティック) PnP マネージャー、ジョイスティックの devnode を作成します。 この時点では、ジョイスティックが構成されている唯一のドライバーは、ジョイスティックの PDO を作成した親 USB ハブ バス ドライバーです。 省略可能なバス フィルター ドライバーは、デバイス スタック内に存在になりますが、例では、わかりやすくするためのバス フィルター ドライバーが省略されます。

    前の図では、2 つの devnode 間のワイド矢印は、ジョイスティック devnode が USB ハブ devnode の子であることを示します。

2.  PnP マネージャーでは、新しいデバイスに関する情報を収集し、デバイスの構成を開始します。

    PnP マネージャーでは、デバイスに関する情報を収集するために、デバイス スタックを Irp のシーケンスを送信します。 この時点では、デバイス スタックは、デバイスの親のバス ドライバーとバスの省略可能なフィルター ドライバーのフィルターを DOs によって作成された PDO のみで構成されます。 そのため、バス ドライバー、バス フィルター ドライバーは、これらの Irp に応答するだけのドライバーです。 この例では、ジョイスティック デバイス スタックでのみ、ドライバーは、親のバス ドライバー、USB ハブのドライバーです。

    PnP マネージャーは、デバイス スタックに Irp を送信することによって、新しいデバイスに関する情報を収集します。 これらの Irp を以下に示します。

    -   [**IRP\_MN\_クエリ\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)のハードウェア Id の次の種類ごとの個別の IRP:

        **BusQueryDeviceID**

        **BusQueryInstanceID**

        **BusQueryHardwareIDs**

        **BusQueryCompatibleIDs**

        **BusQueryContainerID**

    -   [**IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

    -   [**IRP\_MN\_クエリ\_デバイス\_テキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)、次の項目ごとの個別の IRP:

        **DeviceTextDescription**

        **DeviceTextLocationInformation**

    -   [**IRP\_MN\_クエリ\_BUS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)
    -   [**IRP\_MN\_クエリ\_リソース**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)
    -   [**IRP\_MN\_クエリ\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)

    PnP マネージャーが、新しい PnP デバイスの処理のこの段階で上に示した Irp を送信しますが、必ずしも表示されている順番で、そのためことは避けてください Irp が送信される注文に関する前提条件。 また、ことを想定しないでください PnP マネージャーから上に示した Irp のみを送信することです。

    PnP マネージャーは、このコンピューターで、デバイスを既にインストールされているかどうかを確認するレジストリを確認します。 PnP マネージャー チェック、 &lt;*列挙子*&gt;\\&lt;*deviceID* &gt;  の下のサブキー、 **列挙型**分岐します。 この例で、デバイスが新しいし、"ゼロ"から構成する必要があります。

3.  PnP マネージャーでは、レジストリのデバイスに関する情報を格納します。

    レジストリの**Enum**ブランチは、オペレーティング システム コンポーネントによって使用するため予約されており、レイアウトが変更される可能性が。 ドライバーの作成者は、ドライバーに関連する情報を抽出するのにシステム ルーチンを使用する必要があります。 アクセスしない、 **Enum**ドライバーから直接分岐します。 次**Enum**情報は、デバッグ目的でのみ表示されます。

    -   PnP マネージャーでは、デバイスの列挙子のデバイス キーの下のサブキーを作成します。

        PnP マネージャーという名前のサブキーを作成する**HKLM\\システム\\CurrentControlSet\\Enum\\** &lt;*列挙子*&gt; **\\** &lt; *deviceID*&gt;します。 作成、 &lt;*列挙子*&gt;サブキーが既に存在しない場合。

        *列挙子*は PnP デバイスを検出するコンポーネントを標準のプラグ アンド プレイ ハードウェアに基づいています。 列挙子のタスクは、PnP マネージャーとのパートナーシップでの PnP バス ドライバーによって実行されます。 デバイスは通常、PCI や PCMCIA など、その親バス ドライバーによって列挙されます。 ACPI などの bus フィルター ドライバーでは、一部のデバイスが列挙されます。

    -   PnP マネージャーでは、デバイスのこのインスタンスのサブキーを作成します。

        場合**Capabilities.UniqueID**として返される**TRUE**の**IRP\_MN\_クエリ\_機能**デバイスの一意の ID はシステム全体で一意です。 それ以外の場合は、一意なシステム全体をあるように、PnP マネージャーが、ID を変更します。

        PnP マネージャーという名前のサブキーを作成する**HKLM\\システム\\CurrentControlSet\\Enum\\** &lt;*列挙子*&gt; **\\** &lt; *deviceID* &gt; **\\** &lt; *instanceID*&gt;します。

    -   PnP マネージャーでは、デバイスのインスタンスのサブキーに、デバイスに関する情報を書き込みます。

        PnP マネージャーでは、場合は、デバイスの提供されたときに、次を含む情報を格納します。

        **DeviceDesc** — から[ **IRP\_MN\_クエリ\_デバイス\_テキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)

        **場所** — から**IRP\_MN\_クエリ\_デバイス\_テキスト**

        **機能** — からフラグ[ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

        **UINumber** — から**IRP\_MN\_クエリ\_機能**

        **HardwareID** — から[ **IRP\_MN\_クエリ\_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)

        **CompatibleIDs** — から**IRP\_MN\_クエリ\_ID**

        **ContainerID** — から**IRP\_MN\_クエリ\_ID**

        **LogConf\\BootConfig** — from [**IRP\_MN\_QUERY\_RESOURCES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)

        **LogConf\\BasicConfigVector** — from [**IRP\_MN\_QUERY\_RESOURCE\_REQUIREMENTS**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)

この時点では、PnP マネージャーは、関数のドライバーを見つけて、デバイスのドライバーをフィルター処理する準備が存在する場合です。 (詳しくは、次の図を参照してください)。

![図に示すの検索関数とフィルター ドライバー](images/finddrv.png)

次のノートでは、前の図の番号付きの円に対応しています。

1.  カーネル モードの PnP マネージャーは、いずれかを使用する必要がある場合、デバイスの場合、関数とフィルター ドライバーを検索するには、ユーザー モードの PnP マネージャーとユーザー モードのセットアップ コンポーネントと連携します。

    カーネル モードの PnP マネージャーはキューにイベントをインストールする必要があるデバイスを識別する、ユーザー モードの PnP マネージャーです。 特権を持つユーザーがログインすると、ユーザー モード コンポーネントは、ドライバーの検索を続行します。 参照してください、[デバイス インストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)セットアップ コンポーネントと、デバイスのインストールでのロールについて。

2.  ユーザー モードのセットアップ コンポーネントは、関数とフィルター ドライバーが読み込まれるカーネル モードの PnP マネージャーを指示します。

    ユーザー モード コンポーネントが原因で読み込まれると、ドライバーを取得するカーネル モードにコールバックして、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)呼び出されるルーチンをします。

次の図は、PnP マネージャー (適切な) 場合、ドライバーの読み込みを呼び出す、 *AddDevice*ルーチン、およびデバイスを起動するドライバーを指定します。

![ダイアグラム: 呼び出し元 adddevice ルーチンで、新しいデバイスの開始](images/addstart.png)

次のノートでは、前の図の番号付きの円に対応しています。

1.  低いフィルター ドライバー

    関数のドライバーは、デバイス スタックをアタッチ、前に、PnP マネージャーは、低いフィルター ドライバーを処理します。 各下位フィルター ドライバー、PnP マネージャーの呼び出し、ドライバーの[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン、ドライバーがまだ読み込まれていない場合。 ドライバーの PnP マネージャーし*AddDevice*ルーチン。 その*AddDevice* 、日常的なフィルター ドライバー (フィルター操作を行います) フィルター デバイス オブジェクトを作成し、デバイス スタックにアタッチします ([**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack))。 そのデバイス オブジェクトをアタッチしますデバイス スタックをドライバーがデバイスのドライバーとして進行中です。

    USB ジョイスティックの例では、デバイスの 1 つの下位フィルター ドライバーです。

2.  関数のドライバー

    下のすべてのフィルターが接続されると、PnP マネージャーは、関数のドライバーを処理します。 PnP マネージャーには、関数のドライバーの**DriverEntry**ドライバーがまだ読み込まれていないと、呼び出す関数のドライバーの場合、ルーチン*AddDevice*ルーチン。 関数のドライバーでは、関数デバイス オブジェクト (FDO) を作成し、デバイス スタックにアタッチします。

    この例では関数のドライバーを USB ジョイスティックは実際にドライバーのペアです。 HID クラス ドライバーと HID miniclass ドライバー。 2 つのドライバーが連携して機能ドライバーとして機能します。 ドライバーのペアは、1 つだけ FDO を作成し、デバイス スタックにアタッチします。

3.  上位フィルター ドライバー

    関数のドライバーが接続されると、PnP マネージャーは、上位フィルター ドライバーを処理します。

    この例では、デバイスの 1 つの上位フィルター ドライバーです。

4.  リソースを割り当てると、デバイスの開始

    PnP マネージャーは、必要な場合は、リソースをデバイスに割り当てられます。 し、デバイスの起動は IRP を発行します。

    -   リソースの割り当て

        、構成プロセスの前半では、PnP マネージャーは、デバイスの親のバス ドライバーから、デバイスのハードウェア リソース要件を収集します。 PnP マネージャーが送信するデバイスのドライバーの完全なセットが読み込まれた後、 [ **IRP\_MN\_フィルター\_リソース\_要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)要求デバイス スタック。 スタック内のすべてのドライバーでは、この IRP を処理し、必要に応じて、デバイスのリソース要件のリストを変更する機会があります。

        PnP マネージャーでは、リソースを割り当てます、デバイスをデバイスには、いずれかが必要とする場合、デバイスの要件と現在使用可能なリソースに基づきます。

        PnP マネージャーは、既存のデバイスを新しいデバイスのニーズを満たすためのリソースの割り当てを変更する必要があります。 この再割り当てのリソースは「再調整します」と呼ばれる 既存のデバイスのドライバーは stop のシーケンスが表示されの再調整中に Irp を開始しますがの再調整は、ユーザーに対して透過的である必要があります。

        USB スティックの例では、USB デバイス必要はありませんハードウェア リソース PnP マネージャーでは、リソースの一覧を設定ように**NULL**します。

    -   デバイスを起動 (**IRP\_MN\_開始\_デバイス**)

        PnP マネージャーでは、デバイスにリソースを割り当てます、その送信を[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) IRP デバイス スタックを開始するドライバーに出力するため、デバイスです。

    デバイスが開始されると、PnP マネージャーは、次の 3 つ以上の Irp をデバイスのドライバーに送信します。

    -   [**IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

        PnP マネージャーでは IRP が正常に完了すると、開始後に送信別**IRP\_MN\_クエリ\_機能**IRP デバイス スタックをします。 デバイスのすべてのドライバーでは、IRP の処理のオプションがあります。 PnP マネージャーは、関数またはフィルター ドライバーは、機能の情報を収集するデバイスにアクセスする必要がありますので、すべてのドライバーが接続されているし、デバイスが起動した後、この時点でこの IRP を送信します。

    -   [**IRP\_MN\_クエリ\_PNP\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)

        この IRP では、たとえば、レポートなど、デバイスを Device Manager とホットプラグ プログラムなどのユーザー インターフェイスに表示されないことに、ドライバー、営業案件を示します。 これは、システム上に存在するが、ラップトップがドッキングされていないときに、使用できないラップトップのゲーム ポートなど、現在の構成では使用できないデバイスの場合に役立ちます。

    -   [**IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)のバスの関係

        PnP マネージャーは、デバイスのすべての子デバイスがあるかどうかを判断するには、この IRP を送信します。 そうである場合、PnP マネージャーは、それぞれの子デバイスを構成します。

 
## <a name="using-guidpnplocationinterface"></a>GUID_PNP_LOCATION_INTERFACE を使用します。

GUID_PNP_LOCATION_INTERFACE インターフェイスには、SPDRP_LOCATION_PATHS プラグ アンド プレイ (PnP) デバイスのデバイスのプロパティが用意されています。

ドライバーをこのインターフェイスを実装する処理に InterfaceType IRP_MN_QUERY_INTERFACE IRP GUID_PNP_LOCATION_INTERFACE を = です。 ドライバーは、インターフェイスの個々 のルーチンへのポインターを格納する PNP_LOCATION_INTERFACE 構造体へのポインターを提供します。 [PnpGetLocationString ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pget_location_string)SPDRP_LOCATION_PATHS のデバイスのプロパティのデバイスに固有の一部を提供します。



 




