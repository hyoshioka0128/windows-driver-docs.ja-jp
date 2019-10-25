---
title: UMDF 1 から UMDF 2 へのドライバーの移植
description: このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) 1 ドライバーを UMDF 2 に移植する方法について説明します。
ms.assetid: 99D20B4C-17C4-42AC-B4D9-F5FD64E10723
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c9231ab2c56167c2f2b245dfecc990ea812bab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827248"
---
# <a name="porting-a-driver-from-umdf-1-to-umdf-2"></a>UMDF 1 から UMDF 2 へのドライバーの移植


このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) 1 ドライバーを UMDF 2 に移植する方法について説明します。 (Visual Studio プロジェクトではなく) ソース/ディレクトリファイルを使用する UMDF 1 ドライバーから始めることができます。また、Visual Studio プロジェクトに含まれている UMDF 1 ドライバーを変換することもできます。 結果は、Visual Studio の UMDF 2 ドライバープロジェクトになります。 UMDF 2 ドライバーは、Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows 10 Mobile の両方で実行されます。

Echo driver サンプルは、UMDF 1 から UMDF 2 に移植されたドライバーの例です。

-   [Echo サンプル (UMDF バージョン 1)](https://go.microsoft.com/fwlink/p/?LinkId=617707)
-   [Echo サンプル (UMDF バージョン 2)](https://go.microsoft.com/fwlink/p/?LinkId=617708)

## <a name="getting-started"></a>作業の開始


まず、Visual Studio で新しいドライバープロジェクトを開きます。 **Visual C++&gt;Windows DRIVER-&gt;WDF-&gt;User MODE Driver (UMDF 2)** テンプレートを選択します。 Visual Studio では、部分的に設定されたテンプレートが開き、ドライバーが実装する必要のあるコールバック関数のスタブが含まれます。 この新しいドライバープロジェクトは、UMDF 2 ドライバーの基礎となります。 使用するコードの種類については、UMDF 2 Echo サンプルを参考にしてください。

次に、既存の UMDF 1 ドライバーコードを確認し、オブジェクトマッピングを決定します。 UMDF 1 の各 COM オブジェクトには、UMDF 2 に対応する WDF オブジェクトがあります。 たとえば、 **Iwdfdevice**インターフェイスは、wdfdevice ハンドルによって表される WDF device オブジェクトにマップされます。 UMDF 1 でフレームワークによって提供されるほとんどすべてのインターフェイスメソッドには、UMDF 2 の対応するメソッドがあります。 たとえば、 [**Iwdfdevice:: GetDefaultIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultioqueue)は[**WdfDeviceGetDefaultQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)にマップされます。

同様に、ドライバーによって提供されるコールバック関数は、2つのバージョンに相当します。 UMDF 1 では、ドライバーによって提供されるインターフェイス ( **Idriverentry**を除く) の名前付け規則は*I*オブジェクト*コールバック*Xxx ですが、umdf 2 では、ドライバーによって<strong>提供されるルーチンの名前付け規則は *.evt*objectxxx</strong>です。 たとえば、 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバックメソッドは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)にマップされます。

ドライバーは、UMDF 1 と2の両方でコールバック関数を実装しますが、ドライバーがコールバックへのポインターを提供する方法は異なります。 UMDF 1 では、ドライバーによって提供されるインターフェイスのメンバーとしてコールバックメソッドが実装されます。 このドライバーは、 [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出すなどして、フレームワークオブジェクトを作成するときにこれらのインターフェイスをフレームワークに登録します。

UMDF 2 では、ドライバーが提供するドライバーのコールバック関数へのポインターが、 [**WDF\_driver\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)や[**WDF\_IO\_QUEUE\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)などの構成構造に含まれています。

## <a name="managing-object-lifetime"></a>オブジェクトの有効期間の管理


UMDF 1 を使用するドライバーは、オブジェクトを安全に削除できるかどうかを判断するために、参照カウントを実装する必要があります。 フレームワークはドライバーの代わりにオブジェクト参照を追跡するため、UMDF 2 ドライバーは参照をカウントする必要がありません。

UMDF 2 では、各フレームワークオブジェクトに既定の親オブジェクトがあります。 親オブジェクトが削除されると、フレームワークによって、関連付けられている子オブジェクトが削除されます。 ドライバーが[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)などのオブジェクトの作成方法を呼び出すと、既定の親を受け入れることができます。また、 [**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)の構造体でカスタムの親を指定することもできます。 フレームワークオブジェクトとその既定の親オブジェクトの一覧については、「 [Framework オブジェクトの概要](summary-of-framework-objects.md)」を参照してください。

## <a name="driver-initialization"></a>ドライバーの初期化


UMDF 1 ドライバーは、 [**Idriverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)インターフェイスを実装します。 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバックメソッドでは、ドライバーは通常次のようになります。

-   デバイスコールバックオブジェクトのインスタンスを作成して初期化します。
-   [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出すことによって、新しいフレームワークデバイスオブジェクトを作成します。
-   デバイスのキューとそれに対応するコールバックオブジェクトを設定します。
-   [**Iwdfdevice:: CreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)を呼び出すことによって、デバイスインターフェイスクラスのインスタンスを作成します。

UMDF 2 ドライバーは[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)と[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)を実装します。 その**Driverentry**ルーチンでは、通常、UMDF 2 ドライバーは[**WDF\_driver\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdf_driver_config_init)を呼び出して、ドライバーの[**WDF\_driver\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体を初期化します。 次に、この構造体を[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)に渡します。

[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)関数では、ドライバーが次の一部を実行する場合があります。

-   [Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体に入力します。これにより、デバイスオブジェクトの作成に使用される情報が提供されます。 WDFDEVICE\_INIT の使用方法の詳細については、「 [Framework デバイスオブジェクトの作成](creating-a-framework-device-object.md)」を参照してください。
-   デバイスオブジェクトのコンテキスト領域を設定します。 フレームワークオブジェクトのコンテキスト空間の割り当てとアクセスについては、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。
-   [デバイスオブジェクトを作成](creating-a-framework-device-object.md)します。
-   デバイスオブジェクトの[要求ハンドラー](request-handlers.md)を指定します。
-   [I/o キューを作成](creating-i-o-queues.md)します。
-   [デバイスインターフェイスを作成](using-device-interfaces.md)します。
-   デバイスオブジェクトが電源ポリシーを所有している場合は、[デバイスのアイドルポリシー](supporting-idle-power-down.md)と[ウェイク設定](supporting-system-wake-up.md)を設定します。
-   割り込み[オブジェクトを作成](creating-an-interrupt-object.md)します (ハードウェアで割り込みがサポートされている場合)。

## <a name="installing-your-driver"></a>ドライバーのインストール


Visual Studio で新しいドライバープロジェクトを作成すると、新しいプロジェクトには inx ファイルが含まれます。 ドライバーをビルドすると、Visual Studio は、ドライバーパッケージの一部として使用できる INF ファイルに inx ファイルをコンパイルします。

UMDF 1 ドライバーの INF ファイルにはドライバークラス ID を含める必要がありますが、UMDF 2 ドライバーの INF ファイルでは DriverCLSID は必要ありません。

また、UMDF 1 ドライバーは、その INF ファイル内の共同インストーラーを参照する必要がありますが、UMDF 2 INF ファイルでは constaller 参照を必要としません。 の共同インストーラー参照は、UMDF 2 ドライバーの INF ファイルに表示できますが、必須ではありません。

## <a name="storing-device-context"></a>デバイスコンテキストの格納


UMDF 1 では、通常、ドライバーによって作成されたコールバックオブジェクトにデバイスコンテキストが格納されます。たとえば、デバイスコールバックオブジェクトクラスのプライベートメンバーを指定します。 また、UMDF 1 ドライバーは、 [**Iwdfobject:: 割り当てコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)メソッドを呼び出して、フレームワークオブジェクトにコンテキストを登録できます。

UMDF 2 では、フレームワークは、オプションの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)の構造に基づいて、オブジェクトの作成メソッドを呼び出すときにドライバーが提供するコンテキスト空間を割り当てます。 オブジェクトの create メソッドを呼び出した後、ドライバーは[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)を1回以上呼び出して、特定のオブジェクトに追加のコンテキスト空間を割り当てることができます。 UMDF 2 ドライバーがコンテキスト構造とアクセサーメソッドを定義するために使用する手順については、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

## <a name="debugging-your-driver"></a>ドライバーのデバッグ


UMDF 2 ドライバーをデバッグするには、Wudfext dll ではなく、Wdfkd .dll の拡張機能を使用します。 Wudfext dll の拡張機能の詳細については、「 [Wdfkd のデバッガー拡張機能の概要](debugger-extensions-for-kmdf-drivers.md)」を参照してください。

UMDF 2 では、「 [KMDF と UMDF 2 ドライバーでの Inflight トレースレコーダーの使用](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)」で説明されているように、Inflight トレースレコーダー (IFR) を介して追加のドライバーデバッグ情報を取得することもできます。 また、フレームワーク独自の*インフライトレコーダー* (IFR) を使用することもできます。 「[フレームワークのイベントロガーの使用」を](using-the-framework-s-event-logger.md)参照してください。

## <a name="related-topics"></a>関連トピック


[UMDF の概要](getting-started-with-umdf-version-2.md)

[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)

[UMDF バージョン履歴](umdf-version-history.md)

[フレームワークオブジェクト](framework-objects.md)

 

 






