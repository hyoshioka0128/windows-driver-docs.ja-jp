---
title: 実行中システムへの PnP デバイスの追加
description: 実行中システムへの PnP デバイスの追加
ms.assetid: 73d14ba1-6cf1-44eb-8a98-8c2fe44c11bb
keywords:
- PnP WDK カーネル、実行中のシステムへのデバイスの追加
- WDK カーネルのプラグアンドプレイ、実行中のシステムへのデバイスの追加
- 実行中のシステムに PnP デバイスを追加しています
- PnP デバイスの列挙 WDK の PnP
- PnP デバイスのレポート
- devnodes WDK PnP
- デバイスノード WDK PnP
- 関数ドライバー WDK PnP
- ドライバーのフィルターの WDK PnP
- AddDevice ルーチン WDK PnP
- Irp WDK PnP
- I/o 要求パケットの WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3356e859528548243123779c35cf828b1704c6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828674"
---
# <a name="adding-a-pnp-device-to-a-running-system"></a>実行中システムへの PnP デバイスの追加





このセクションでは、ユーザーが実行中のコンピューターに追加した PnP デバイスをシステムが構成するときに発生する一連のイベントについて説明します。 ここでは、新しいデバイスの列挙と構成における PnP マネージャー、バスドライバー、および関数とフィルタードライバーの役割について説明します。

この説明のほとんどは、コンピューターの起動時に存在する PnP デバイスの構成にも関連しています。 具体的には、ドライバーが SERVICE\_\_とマークされているデバイスは、デバイスを動的に追加するか、起動時に存在するかにかかわらず、基本的には同じように構成されます。

次の図は、ユーザーがハードウェアをコンピューターに接続したときから、デバイスを構成するための最初の手順を示しています。

![プラグアンドプレイデバイスの列挙とレポートを示す図](images/hotplug.png)

次の注意事項は、前の図の丸で囲まれた数値に対応しています。

1.  ユーザーが pnp バスの空きスロットに PnP デバイスを接続します。

    この例では、ユーザーが PnP USB ジョイスティックを USB ホストコントローラーのハブに接続します。 USB ハブは、子デバイスを接続できるため、PnP バスデバイスです。

2.  バスデバイスの関数ドライバーによって、新しいデバイスがバス上にあることが判断されます。

    ドライバーがこれを決定する方法は、バスアーキテクチャによって異なります。 一部のバスでは、バス関数ドライバーは新しいデバイスのホットプラグ通知を受け取ります。 バスがホットプラグ通知をサポートしていない場合は、ユーザーはコントロールパネルで適切な操作を行って、バスが列挙されるようにする必要があります。

    この例では、USB バスはホットプラグ通知をサポートしているので、USB バスの関数ドライバーには、その子が変更されたことが通知されます。

3.  バスデバイスの関数ドライバーは、子デバイスのセットが変更されたことを PnP マネージャーに通知します。

    関数ドライバーは、 **Busrelations***型*の[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出すことによって、PnP マネージャーに通知します。

4.  PnP マネージャーは、バスのドライバーに対して、バス上の現在のデバイスの一覧を照会します。

    PnP マネージャーは、 [**IRP\_\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)要求をバスのデバイススタックに送信します。 **QueryDeviceRelations**値は**busrelations**で、これは、PnP マネージャーがバス上に存在するデバイスの現在の一覧を要求していることを示しています (*バス関係*)。

    PnP マネージャーは、バスのデバイススタックの最上位のドライバーに IRP を送信します。 PnP Irp のルールに従って、スタック内の各ドライバーは、必要に応じて IRP を処理し、次のドライバーに IRP を渡します。

5.  バスデバイスの関数ドライバーは、IRP を処理します。

    この IRP の処理の詳細については、「 [**irp\_\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)」の参照ページを参照してください。

    この例では、USB ハブドライバーはハブ*FDO*に対してこの IRP を処理します。 ハブドライバーは、ジョイスティックデバイス用の*PDO*を作成し、IRP と共に返される子デバイスの一覧に、ジョイスティック PDO への参照先ポインターを含めます。

    USB ハブの親バスドライバー (USB ホストコントローラークラス/miniclass ドライバーペア) が IRP を完了すると、IRP はハブドライバーによって登録された[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを使って、デバイススタックをバックアップします。

バス関数ドライバーは、子デバイスの一覧を PnP マネージャーが照会するように要求することによって、子の一覧の変更を報告します。 生成される**IRP\_\_クエリ\_デバイス\_関係**要求は、バスデバイスのすべてのドライバーによって示されます。 通常、バス関数ドライバーは、IRP とレポートの子を処理する唯一のドライバーです。 一部のデバイススタックでは、バスフィルタードライバーが存在し、バス関係の一覧の構築に参加します。 1つの例として、acpi デバイス用のバスフィルタードライバーとしてアタッチされる ACPI があります。 一部のデバイススタックでは、nonbus フィルタードライバーは、**デバイス\_関係要求\_の IRP\_\_クエリ**を処理しますが、これは一般的ではありません。

この時点で、PnP マネージャーにはバス上のデバイスの現在の一覧があります。 PnP マネージャーは、デバイスが新しく到着したか削除されたかを判断します。 この例では、新しいデバイスが1つあります。 次の図は、新しいデバイスの devnode を作成し、デバイスの構成を開始する PnP マネージャーを示しています。

![新しいプラグアンドプレイデバイス用の devnode の作成を示す図](images/credvnd.png)

次の注意事項は、前の図の丸で囲まれた数値に対応しています。

1.  PnP マネージャーは、バス上の新しい子デバイスの devnodes を作成します。

    PnP マネージャーは、 **irp\_\_クエリ\_デバイス\_relations** irp で返されたバスリレーションの一覧を、現在 PnP デバイスツリーに記録されているバスの子の一覧と比較します。 PnP マネージャーは、新しいデバイスごとに devnode を作成し、削除されたすべてのデバイスの削除処理を開始します。

    この例では、1つの新しいデバイス (ジョイスティック) があるため、PnP マネージャーはジョイスティックの devnode を作成します。 この時点で、ジョイスティック用に構成されている唯一のドライバーは、ジョイスティックの PDO を作成した親の USB hub バスドライバーです。 オプションのバスフィルタードライバーもデバイススタックに存在しますが、この例では、わかりやすくするためにバスフィルタードライバーを省略しています。

    前の図の2つの devnodes の間のワイド矢印は、ジョイスティック devnode が USB ハブ devnode の子であることを示しています。

2.  PnP マネージャーは、新しいデバイスに関する情報を収集し、デバイスの構成を開始します。

    PnP マネージャーは、デバイススタックに一連の Irp を送信し、デバイスに関する情報を収集します。 この時点で、デバイススタックは、デバイスの親バスドライバーによって作成された PDO だけで構成され、任意のオプションのバスフィルタードライバーに対して DOs をフィルター処理します。 そのため、これらの Irp に応答するドライバーは、バスドライバーとバスフィルタードライバーだけです。 この例では、ジョイスティックデバイススタック内の唯一のドライバーは、親バスドライバーである USB ハブドライバーです。

    PnP マネージャーは、デバイススタックに Irp を送信することによって、新しいデバイスに関する情報を収集します。 これらの Irp には、次のものが含まれます。

    -   Irp は、次の種類のハードウェア Id それぞれに対して個別の IRP である、[**クエリ\_ID を\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)します。

        **BusQueryDeviceID**

        **BusQueryInstanceID**

        **Busqueryハードウェア Id**

        **Busquery互換 Id**

        **BusQueryContainerID**

    -   [**IRP\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

    -   Irp は、次の各項目に対して個別の IRP である[**デバイス\_テキストを\_\_クエリを\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)します。

        **DeviceTextDescription**

        **DeviceTextLocationInformation**

    -   [**IRP\_\_クエリ\_バス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)
    -   [**IRP\_\_クエリ\_リソース**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)
    -   [**IRP\_\_クエリ\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)

    PnP マネージャーは、上に示した Irp を、新しい PnP デバイスの処理のこの段階で送信しますが、必ずしも一覧に記載されているものではありません。したがって、Irp が送信される順序については想定しないでください。 また、PnP マネージャーが上記の Irp だけを送信することを想定しないでください。

    PnP マネージャーは、以前にデバイスがこのコンピューターにインストールされているかどうかを確認するために、レジストリを確認します。 PnP マネージャーは、 **Enum**分岐の下にあるデバイスの&gt;\\&lt;*deviceID*&gt; サブキーを &lt;*列挙子*を確認します。 この例では、デバイスは新しいので、"ゼロから" 構成する必要があります。

3.  PnP マネージャーは、デバイスに関する情報をレジストリに格納します。

    レジストリの**Enum**分岐はオペレーティングシステムコンポーネントで使用するために予約されており、そのレイアウトは変更される可能性があります。 ドライバーライターは、ドライバーに関連する情報を抽出するためにシステムルーチンを使用する必要があります。 ドライバーから直接**列挙**分岐にアクセスしないでください。 次の**列挙**情報は、デバッグ目的でのみ表示されます。

    -   PnP マネージャーは、デバイスの列挙子のキーの下にデバイスのサブキーを作成します。

        PnP マネージャーは、 **HKLM\\System\\CurrentControlSet\\Enum\\** &lt;*列挙子* **&gt;\\&lt;** *deviceID*&gt;という名前のサブキーを作成します。 まだ存在しない場合は、&lt;*列挙子*&gt; サブキーが作成されます。

        *列挙子*は、pnp ハードウェア標準に基づいて pnp デバイスを検出するコンポーネントです。 列挙子のタスクは、pnp マネージャーとのパートナーシップで PnP バスドライバーによって実行されます。 通常、デバイスは、PCI や PCMCIA などの親バスドライバーによって列挙されます。 一部のデバイスは、ACPI などのバスフィルタードライバーによって列挙されます。

    -   PnP マネージャーによって、デバイスのこのインスタンスのサブキーが作成されます。

        **機能し**ている場合は、 **IRP\_\_クエリ\_機能**については**TRUE**として返されます。デバイスの一意の ID は、システム全体で一意です。 そうでない場合は、システム全体で一意になるように、PnP マネージャーによって ID が変更されます。

        PnP マネージャーによって、 **HKLM\\System\\CurrentControlSet\\Enum\\** &lt;*enumerator* **&gt;\\** &lt;*deviceID*&gt;という名前のサブキーが作成され **\\** *instanceID*&gt;を&lt;します。

    -   PnP マネージャーは、デバイスに関する情報をデバイスインスタンスのサブキーに書き込みます。

        PnP マネージャーは、デバイスに指定されている場合、次のような情報を格納します。

        **DeviceDesc** — [ **IRP\_\_クエリ\_デバイス\_テキスト**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)

        **場所** — **IRP\_\_クエリ\_デバイス\_テキスト**

        **機能** — IRP からのフラグ[ **\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

        **Uinumber** — **IRP\_\_クエリ\_機能**から

        **HardwareID** — [ **IRP\_\_クエリ\_ID**から](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)

        ** -** **IRP\_からの\_のクエリ\_ID**

        **ContainerID** — **IRP から\_の\_クエリ\_ID**

        **Logconf\\BootConfig** - [ **IRP\_の\_クエリ\_リソース**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)

        **Logconf\\BasicConfigVector** - [ **IRP\_の\_クエリ\_リソース\_の要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)

この時点で、PnP マネージャーはデバイスの関数ドライバーとフィルタードライバーを見つける準備ができています。 (次の図を参照してください)。

![関数とフィルタードライバーの検索を示す図](images/finddrv.png)

次の注意事項は、前の図の番号付き円に対応しています。

1.  カーネルモードの PnP マネージャーは、ユーザーモードの PnP マネージャーとユーザーモードのセットアップコンポーネントを調整して、デバイスの関数とフィルタードライバー (存在する場合) を検索します。

    カーネルモードの PnP マネージャーは、インストールする必要があるデバイスを識別するために、ユーザーモードの PnP マネージャーにイベントをキューに配置します。 特権を持つユーザーがログインすると、ユーザーモードのコンポーネントはドライバーの検索に進みます。 デバイスの[インストール](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)におけるセットアップコンポーネントとその役割の詳細については、「デバイスのインストールの概要」を参照してください。

2.  ユーザーモードセットアップコンポーネントは、カーネルモードの PnP マネージャーに対して、関数とフィルタードライバーの読み込みを指示します。

    ユーザーモードコンポーネントはカーネルモードに戻り、ドライバーが読み込まれるようにして、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。

次の図は、ドライバーを読み込んで (該当する場合)、 *AddDevice*ルーチンを呼び出し、デバイスを起動するようにドライバーを指示する PnP マネージャーを示しています。

![adddevice ルーチンの呼び出しと新しいデバイスの開始を示す図](images/addstart.png)

次の注意事項は、前の図の番号付き円に対応しています。

1.  下位フィルタードライバー

    関数ドライバーがデバイススタックにアタッチされる前に、PnP マネージャーは、すべての下位フィルタードライバーを処理します。 ドライバーがまだ読み込まれていない場合は、ドライバーが下位のドライバーごとにドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 PnP マネージャーは、ドライバーの*AddDevice*ルーチンを呼び出します。 この*AddDevice*ルーチンでは、フィルタードライバーによってフィルターデバイスオブジェクト (フィルター処理) が作成され、デバイススタック ([**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)) にアタッチされます。 デバイスオブジェクトをデバイススタックに接続すると、ドライバーはデバイスのドライバーとして使用されます。

    USB ジョイスティックの例には、デバイス用の下位フィルタードライバーが1つあります。

2.  関数ドライバー

    より低いフィルターがアタッチされると、PnP マネージャーによって関数ドライバーが処理されます。 ドライバーがまだ読み込まれていない場合は、PnP マネージャーが関数ドライバーの**Driverentry**ルーチンを呼び出し、関数ドライバーの*AddDevice*ルーチンを呼び出します。 関数ドライバーは、関数デバイスオブジェクト (FDO) を作成し、デバイススタックにアタッチします。

    この例では、USB ジョイスティックの関数ドライバーは実際には、HID クラスドライバーと HID miniclass driver というドライバーのペアです。 2つのドライバーが連携して、関数ドライバーとして機能します。 ドライバーペアは、FDO を1つだけ作成し、デバイススタックにアタッチします。

3.  上位フィルタードライバー

    関数ドライバーがアタッチされると、PnP マネージャーは上位フィルタードライバーをすべて処理します。

    この例では、デバイス用の上位フィルタードライバーが1つあります。

4.  リソースの割り当てとデバイスの起動

    PnP マネージャーは、必要に応じて、デバイスにリソースを割り当て、デバイスを起動するための IRP を発行します。

    -   リソースの割り当て

        前の構成プロセスでは、PnP マネージャーがデバイスの親バスドライバーからハードウェアリソース要件を収集していました。 デバイスのドライバーの完全なセットが読み込まれると、PnP マネージャーは、デバイススタックに[ **\_リソース\_要件の要求\_フィルター処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)して、IRP\_を送信します。 スタック内のすべてのドライバーは、この IRP を処理し、必要に応じてデバイスのリソース要件の一覧を変更することができます。

        PnP マネージャは、デバイスの要件と現在使用可能なリソースに基づいて、デバイスにリソースを割り当てます。

        PnP マネージャーは、新しいデバイスのニーズを満たすために、既存のデバイスのリソース割り当てを再配置する必要がある場合があります。 このリソースの再割り当ては "再調整" と呼ばれます。 再調整中に、既存のデバイスのドライバーは停止および開始の Irp のシーケンスを受け取りますが、再調整はユーザーに対して透過的に行う必要があります。

        USB ジョイスティックの例では、USB デバイスはハードウェアリソースを必要としないため、PnP マネージャーはリソースリストを**NULL**に設定します。

    -   デバイスを起動しています (**IRP\_が、\_デバイスを開始\_** 。

        PnP マネージャーは、デバイスにリソースを割り当てた後、\_デバイスの irp を起動してデバイススタックに送信し[ **\_irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を送信し、デバイスを起動するようにドライバーに指示します。

    デバイスが起動すると、PnP マネージャーはデバイスのドライバーに次の3つの Irp を送信します。

    -   [**IRP\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

        Start IRP が正常に完了すると、PnP マネージャーは別の**irp\_\_クエリ\_機能**の irp をデバイススタックに送信します。 デバイスのすべてのドライバーには、IRP を処理するオプションがあります。 この IRP は、すべてのドライバーがアタッチされ、デバイスが起動された後に、この IRP を送信します。機能情報を収集するために、関数またはフィルタードライバーがデバイスにアクセスする必要があるためです。

    -   [**IRP\_\_クエリ\_PNP\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)

        この IRP は、たとえば、デバイスがデバイスマネージャーや Hotplug プログラムなどのユーザーインターフェイスに表示されないことを報告する機会をドライバーに与えます。 これは、システム上に存在していても、ラップトップがドッキングされていないときには使用できないラップトップのゲームポートなど、現在の構成では使用できないデバイスに便利です。

    -   バスリレーションに対する[**IRP\_\_クエリ\_デバイス\_関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)

        PnP マネージャーは、デバイスに子デバイスがあるかどうかを判断するために、この IRP を送信します。 その場合は、PnP マネージャーによって各子デバイスが構成されます。

 
## <a name="using-guid_pnp_location_interface"></a>GUID_PNP_LOCATION_INTERFACE の使用

GUID_PNP_LOCATION_INTERFACE インターフェイスは、デバイスの SPDRP_LOCATION_PATHS プラグアンドプレイ (PnP) デバイスプロパティを提供します。

このインターフェイスをドライバーに実装するには、InterfaceType = GUID_PNP_LOCATION_INTERFACE を使用して IRP_MN_QUERY_INTERFACE IRP を処理します。 ドライバーは、インターフェイスの個々のルーチンへのポインターを含む PNP_LOCATION_INTERFACE 構造体へのポインターを提供します。 [PnpGetLocationString ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pget_location_string)は、デバイスの SPDRP_LOCATION_PATHS プロパティのデバイス固有の部分を提供します。



 




