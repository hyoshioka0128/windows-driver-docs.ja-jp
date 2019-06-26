---
title: WDM と WDF の違い
description: WDM モデルは、オペレーティング システムに密接に関連付けられています。
ms.assetid: 4D35F0AB-44CE-49CA-8AB7-3922871567B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f1e3cd36aa053cc68ba7f0ed1df13d7d360a4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377414"
---
# <a name="differences-between-wdm-and-wdf"></a>WDM と WDF の違い


WDM モデルは、オペレーティング システムに密接に関連付けられています。 ドライバーは、システム サービス ルーチンを呼び出すと、オペレーティング システムの構造を操作することによって、オペレーティング システムと直接対話します。 WDM ドライバーは、信頼されたカーネル モードのコンポーネントであるため、システムは、ドライバーの入力の制限のチェックを提供します。

比較では、Windows Driver Frameworks (WDF) モデルは、ドライバーの要件に重点を置いていて、フレームワーク ライブラリが多数のシステムとの対話を処理します。

フレームワークは、I/O 要求をインターセプトは、適切な場所に既定のアクションを実行し、必要に応じて、ドライバーのコールバックを呼び出します。 WDF モデルは、ベース オブジェクトとイベント ドリブンです。 オブジェクトは、デバイス、ロック、またはキューなどの一般的なドライバーの構成要素を表します。 カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) ドライバーには、エントリ ポイントが含まれています ([**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers))、サービスに必要なイベントに関連するコールバック関数、デバイスとサポートの I/O、および実装に依存するすべての内部の他のユーティリティ関数。

このセクションでは、WDM と WDF の間で、次の領域の重要な相違点について説明します。

-   [ドライバー構造](#driver-structure)
-   [デバイス オブジェクトとドライバーの役割](#device-objects-and-driver-roles)
-   [オブジェクト モデル](#object-model)
-   [オブジェクトの作成](#object-creation)
-   [オブジェクト コンテキストの領域](#object-context-area)
-   [サポートされている IRP の種類](#supported-irp-types)
-   [I/O キュー](#io-queues)
-   [同期と同時実行](#synchronization-and-concurrency)
-   [ドライバーのインストール](#driver-installation)

## <a name="driver-structure"></a>ドライバー構造


WDM と WDF の両方のドライバーが含まれて、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンでは、多数の特定の I/O 要求を処理するために呼び出されるルーチンで、さまざまなサポート ルーチン。

WDM ドライバーでは、I/O のディスパッチ ルーチンは、IRP のコードを特定のメジャーにマップします。 ディスパッチ ルーチンは、I/O マネージャーから Irp を受信し、解析したり、適宜対応します。

WDF のドライバー、フレームワークは、I/O マネージャーから Irp を受信し、解析したり、し、それらを処理するために、ドライバーのイベントのコールバック関数を呼び出す独自のディスパッチ ルーチンを登録します。 イベントのコールバック関数は、通常より WDM ドライバーの一般的な I/O ディスパッチ ルーチン固有のタスクを実行します。

プラグ アンド プレイ デバイスの一般的な WDF ドライバーが含まれます。

-   A [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチン。
-   [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)ルーチンで、WDM AddDevice ルーチンの関数と似ています。
-   1 つまたは複数の I/O キュー。
-   1 つまたは複数 I/O イベント コールバック関数、WDM ドライバーの I/O の機能と同じである*DispatchXxx*ルーチン。
-   プラグ アンド プレイし、ドライバーがサポートする電源イベントを処理するためにコールバックします。
-   ドライバーがサポートする WMI 要求を処理するコールバック。 (KMDF のみ)
-   コールバックの追加、必要に応じて、オブジェクトのクリーンアップ、ファイルの作成、および I/O のターゲットをします。

## <a name="device-objects-and-driver-roles"></a>デバイス オブジェクトとドライバーの役割


WDM と WDF の両方のドライバーでは、1 つまたは複数のデバイス オブジェクトを作成します。 各デバイス オブジェクトは、I/O 要求の対象であるドライバー ロールを表します。 物理デバイス オブジェクト (PDO) は、バス ドライバーを表す、機能のデバイス オブジェクト (FDO) 表します関数ドライバー、およびフィルター デバイス オブジェクト (フィルター操作を行います) フィルター ドライバーを表します。

WDM ドライバーでこれらのドライバーの役割が暗黙的に、ドライバーする必要がありますを追跡するロールの各デバイス オブジェクトを表し、Irp を適切に応答するようにします。

WDF ドライバー、ただし、明示的にかを示すデバイス オブジェクトを表す FDO、PDO (KMDF のみ) フィルターは、そのロールに固有のイベントのコールバックを登録します。 などの対象となって Pdo[リソース要件クエリ](creating-a-resource-requirements-list.md)と[の取り出しとデバイスの要求](supporting-ejectable-devices.md)DOs がしない Fdo とフィルターは、このような要求を処理します。

WDF ドライバーは、特定の種類の I/O 要求を受信するには、各デバイス オブジェクトを構成します。 フレームワークは、I/O 要求のみを処理するために、ドライバーの呼び出しをその他のすべての要求の既定のアクションを実行します。 デバイス オブジェクトは、フィルター ドライバーを表している場合、フレームワークは、その他のすべての要求を [次へ] の下のドライバーに渡します。 デバイス オブジェクトは、バスまたは関数のドライバーを表している場合、フレームワークはその他のすべての要求の種類が失敗します。

プラグ アンド プレイと電源の要求は、フレームワークは各デバイス オブジェクトの適切な要求に対してのみ、KMDF ドライバーまたは UMDF ドライバーを呼び出します: と適切な時点。 たとえば、FDO は、基になる PDO が既に応答した後、特定要求に応答する必要があります。 FDO が I/O 完了ルーチンを設定する必要があります WDM ドライバーには、下位のスタック、IRP を渡すし、下位のドライバーの後に処理します。 WDF ドライバーは単に、対応するコールバック ルーチンを実装し、下位のドライバーは処理が完了したら、framework 呼び出しにします。

フレームワークにデバイス オブジェクトを作成する方法については、次を参照してください。 [Framework デバイス オブジェクトを作成する](creating-a-framework-device-object.md)します。

一部のドライバーでは、プラグ アンド プレイの独立した特定の I/O 要求も処理します。 WDM ドライバーは、デバイスを作成します。\_オブジェクトなどのターゲットは、要求が、プラグ アンド プレイ デバイス スタックにはアタッチできません。 KMDF ドライバー、同じ目的を達成する[コントロール デバイス オブジェクトを作成する](using-control-device-objects.md)します。 いくつかのフレームワークに基づいたドライバーの使用は、特定の種類のデバイスの状態に関係なく、I/O 要求を受信できるように、「側波帯」I/O メカニズムを実装するためにデバイス オブジェクトを制御します。

## <a name="object-model"></a>オブジェクト モデル


WDF を一貫性のあるオブジェクトをモデルにオブジェクトのドライバーには見えません、ドライバーが構成可能なコンテキストの領域ハンドルによって参照されるをサポートしています。 WDM オブジェクトは、ドライバーにアクセスし、ポインターによって参照されるシステム全体のオブジェクトです。 WDM オブジェクトが破損したドライバーには、システム全体が破損していることができます。 WDF オブジェクトの破損だけではありませんが難しく —、フレームワーク、ドライバーを提供するデータを検証するためが、システム全体に問題が発生も少なくなります。

KMDF オブジェクトの名前付け規則については、次を参照してください。 [WDF アーキテクチャ](kernel-mode-driver-framework-architecture.md)します。

フレームワークは、その有効期間をある程度の制御により、各オブジェクトの参照カウントを保持します。 詳細については、次を参照してください。 [Framework オブジェクトのライフ サイクル](framework-object-life-cycle.md)します。

WDF オブジェクトの多くは、WDM オブジェクトに対応して、WDF オブジェクトでは、WDM ドライバーの追加コードが必要となる機能をサポートします。 WDF のすべてのオブジェクトは、ドライバーは、オブジェクト自体を持つオブジェクトの特定のインスタンスに関連する情報を格納できるようにドライバー定義可能なオブジェクト コンテキストの領域をサポートします。 オブジェクトは、通常の状態もを追跡します。 たとえば、WDFQUEUE オブジェクトは、I/O 要求の一覧以上複数の種類のディスパッチ、プラグ アンド プレイでは、要求のキャンセルと自動同期をサポートしています。 WDFMEMORY オブジェクト、framework マネージ参照カウント メモリ リークとリソースの早期解放を防止に役立ちます。

## <a name="object-creation"></a>オブジェクトの作成


WDF のドライバーでは、すべての種類のオブジェクトを作成する正規表現パターンに従います。

1.  1 つが存在する場合は、オブジェクトの構成構造を初期化します。
2.  必要に応じて、オブジェクトの属性の構造体を初期化します。
3.  オブジェクトを作成する作成メソッドを呼び出します。

構成構造と属性の構造は、オブジェクトと、ドライバーがそれを使用する方法に関する基本情報を指定します。 すべてのオブジェクトの型の使用[ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)属性として、構造体がオブジェクトの種類ごとの構成構造が異なると、一部のオブジェクトがないです。いずれかであります。 などがありますが、 [ **WDF\_ドライバー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)が構造体、 **WDF\_デバイス\_CONFIG**構造体。

構成構造は、オブジェクトのドライバーのイベントのコールバック関数などのオブジェクトに固有の情報へのポインターを保持します。 ドライバーこの構造体に格納し、し、渡しますフレームワークにオブジェクトの作成方法を呼び出すときに。 呼び出しなど[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)へのポインターが含まれています、 [ **WDF\_ドライバー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)ドライバーへのポインターを含む構造体[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

フレームワークは、WDF をという名前の関数を定義します\_*オブジェクト*\_CONFIG\_INIT 構成構造体を初期化するために、*オブジェクト*を表します。オブジェクトの種類の名前。 [ **WDF\_オブジェクト\_属性\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdf_object_attributes_init)関数は、ドライバーの初期化[ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体。

## <a name="object-context-area"></a>オブジェクト コンテキストの領域


オブジェクトのすべてのインスタンスには、1 つまたは複数のオブジェクト コンテキストの領域を持つことができます。 オブジェクト コンテキストの領域は、イベントのドライバーに割り当てられたオブジェクトなど、特定のインスタンスに関連付けられているデータのストレージ領域です。 ドライバーは、オブジェクト コンテキストの領域のレイアウトとサイズを決定します。 デバイス オブジェクト、オブジェクト コンテキストの領域は WDM デバイス拡張機能のと同じです。 定義して、コンテキストの領域の初期化については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

## <a name="supported-irp-types"></a>サポートされている IRP の種類


WDF は、Windows Irp のサブセットをサポートしています。 主な WDM IRP 型と対応する WDF イベントのコールバック関数の概要については、次を参照してください。 [WDM Irp と WDF イベントのコールバック関数](wdm-irps-and-kmdf-event-callback-functions.md)します。

表に記載されている以外には、ドライバーが Irp を受信すると、場合でも、KMDF に移植することができます。 KMDF は、ドライバーは「生」WDM Irp を受信は、KMDF 機能を使用しても他の種類の Irp のメカニズムを提供します。 詳細については、次を参照してください。[処理 WDM Irp 外側のフレームワーク](handling-wdm-irps-outside-of-the-framework.md)します。

## <a name="io-queues"></a>I/O キュー


ほぼすべてのドライバーでは、I/O 要求をキューします。 WDM ドライバーでは、次の方法のいずれかの通常使用します。

-   実装を[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)関数と呼び出し[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)と[ **います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket) I/O 要求に対して、システムのデバイスのキューを使用します。
-   使用して、 **IoCsqXxx**または内部の I/O キューを実装するには、他のリストの管理機能。
-   使用して、 **KeXxxDeviceQueue**関数を初期化し、スピン ロックで保護されているキューを管理します。

WDF ドライバーは WDF キュー オブジェクトを I/O キューを表す (WDFQUEUE) を作成します。 WDF のキュー オブジェクトは、キャンセルの安全なキューに似ていますが、その他の機能を提供します。

WDM ドライバーを WDF を移植するときに、WDM ドライバーを使用するメカニズムに関係なく WDF のキュー メカニズムを使用することができます。 キューの詳細については、次を参照してください。 [Framework キュー オブジェクト](framework-queue-objects.md)します。

## <a name="synchronization-and-concurrency"></a>同期と同時実行


WDF ドライバーは、つまり WDM ドライバーを使用できないいくつかの組み込みの同期サポートを利用します。 このサポートしないわけでは、ドライバーは、同時実行とデータへの同期アクセス無視することができます、WDF ドライバーそれでもが必要に大幅に少数のロックと WDM ドライバーよりも少ない同期コード。

フレームワークを提供する同期機能の詳細については、次を参照してください。[同期手法](synchronization-techniques-for-wdf-drivers.md)します。

## <a name="driver-installation"></a>ドライバーのインストール


WDM ドライバーなど、KMDF および UMDF ドライバーは、INF ファイルを使用してインストールされます。 ただし、WDF ドライバーのインストールもには、Windows Driver Kit (WDK) で提供されるフレームワーク共同インストーラーが必要です。 共同インストーラーにより、フレームワーク ライブラリの互換性のあるバージョンがターゲット システムに存在するようになります。 インストールについては、次を参照してください。 [WDF ドライバーの読み込みのビルドと](building-and-loading-a-kmdf-driver.md)します。

 

 





