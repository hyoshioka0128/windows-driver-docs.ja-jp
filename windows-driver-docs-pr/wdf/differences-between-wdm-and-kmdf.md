---
title: WDM と WDF の違い
description: WDM モデルは、オペレーティングシステムと密接に結び付いています。
ms.assetid: 4D35F0AB-44CE-49CA-8AB7-3922871567B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0083fd534ad70b35fc850ab937fa9fccd229b2dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823704"
---
# <a name="differences-between-wdm-and-wdf"></a>WDM と WDF の違い


WDM モデルは、オペレーティングシステムと密接に結び付いています。 ドライバーは、システムサービスルーチンを呼び出し、オペレーティングシステムの構造を操作することによって、オペレーティングシステムと直接対話します。 WDM ドライバーは信頼されたカーネルモードコンポーネントであるため、システムはドライバー入力に対して限定的なチェックを行います。

これに対して、Windows ドライバーフレームワーク (WDF) モデルはドライバーの要件に重点を置いており、フレームワークライブラリはシステムとのやり取りの大部分を処理します。

フレームワークは、i/o 要求をインターセプトし、必要に応じて既定のアクションを実行し、必要に応じてドライバーのコールバックを呼び出します。 WDF モデルは、オブジェクトベースでイベントドリブンです。 オブジェクトは、デバイス、ロック、キューなどの一般的なドライバーコンストラクトを表します。 カーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) ドライバーには、エントリポイント ([**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers))、デバイスのサービスと i/o のサポートに必要なイベント関連のコールバック関数、およびその他の内部ユーティリティが含まれています。実装が依存する関数。

このセクションでは、次の領域における WDM と WDF の重要な違いについて説明します。

-   [ドライバーの構造](#driver-structure)
-   [デバイスオブジェクトとドライバーロール](#device-objects-and-driver-roles)
-   [オブジェクトモデル](#object-model)
-   [オブジェクトの作成](#object-creation)
-   [オブジェクトコンテキスト領域](#object-context-area)
-   [サポートされる IRP 型](#supported-irp-types)
-   [I/o キュー](#io-queues)
-   [同期と同時実行](#synchronization-and-concurrency)
-   [ドライバーのインストール](#driver-installation)

## <a name="driver-structure"></a>ドライバーの構造


WDM と WDF の両方のドライバーには、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチン、特定の i/o 要求を処理するために呼び出される多数のルーチン、およびさまざまなサポートルーチンが含まれています。

WDM ドライバーでは、i/o ディスパッチルーチンは特定の主要な IRP コードにマップされます。 ディスパッチルーチンは、i/o マネージャーから Irp を受け取り、解析し、それに応じて応答します。

WDF ドライバーでは、フレームワークによって独自のディスパッチルーチンが登録されます。このルーチンは、i/o マネージャーから Irp を受信して解析し、ドライバーのイベントコールバック関数を呼び出してそれらを処理します。 イベントコールバック関数は、通常、WDM ドライバーの一般的な i/o ディスパッチルーチンよりも具体的なタスクを実行します。

プラグアンドプレイデバイスの一般的な WDF ドライバーには次のものが含まれます。

-   [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチン。
-   [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)ルーチン。これは、関数の中で WDM AddDevice ルーチンに似ています。
-   1つ以上の i/o キュー。
-   1つ以上の i/o イベントコールバック関数。これは、WDM ドライバーの i/o *DispatchXxx*ルーチンと同様に機能します。
-   ドライバーがサポートするプラグアンドプレイおよび電源イベントを処理するコールバック。
-   ドライバーがサポートする WMI 要求を処理するコールバック。 (KMDF のみ)
-   必要に応じて、オブジェクトのクリーンアップ、ファイルの作成、および i/o ターゲットなどの追加のコールバック。

## <a name="device-objects-and-driver-roles"></a>デバイスオブジェクトとドライバーロール


WDM と WDF の両方のドライバーで、1つまたは複数のデバイスオブジェクトが作成されます。 各デバイスオブジェクトは、i/o 要求のターゲットであるドライバーロールを表します。 物理デバイスオブジェクト (PDO) はバスドライバーを表し、機能デバイスオブジェクト (FDO) は関数ドライバーを表し、フィルターデバイスオブジェクト (フィルター) はフィルタードライバーを表します。

WDM ドライバーでは、これらのドライバーの役割は暗黙的なものであるため、ドライバーは、各デバイスオブジェクトが表す役割を追跡し、Irp に適切に応答する必要があります。

ただし、WDF ドライバーは、デバイスオブジェクトが PDO (KMDF のみ)、FDO、または filter DO を表し、そのロールに固有のイベントコールバックを登録するかどうかを明示的に示します。 たとえば、PDOs は[リソース要件のクエリ](creating-a-resource-requirements-list.md)と[デバイスの取り出し要求](supporting-ejectable-devices.md)のターゲットであるのに対し、Fdos とフィルター DOs はこのような要求を処理しません。

WDF ドライバーは、特定の種類の i/o 要求を受信するように各デバイスオブジェクトを構成します。 フレームワークはドライバーを呼び出して、i/o 要求だけを処理し、他のすべての要求に対して既定のアクションを実行します。 デバイスオブジェクトがフィルタードライバーを表している場合、フレームワークは、他のすべての要求を次の下位のドライバーに渡します。 デバイスオブジェクトがバスまたは関数ドライバーを表している場合、フレームワークは他のすべての要求の種類を失敗させることになります。

プラグアンドプレイと電源要求の場合、フレームワークは、各デバイスオブジェクトに適切な要求 (および適切なタイミング) に対してのみ KMDF または UMDF ドライバーを呼び出します。 たとえば、FDO は、基になる PDO が既に応答した後に、特定の要求に応答する必要があります。 WDM ドライバーでは、FDO は i/o 完了ルーチンを設定し、IRP をスタックに渡して、低いドライバーの後に処理する必要があります。 WDF ドライバーは、対応するコールバックルーチンを実装するだけで、低レベルのドライバーが処理を完了した後に、フレームワークはそれを呼び出します。

フレームワークデバイスオブジェクトを作成する方法については、「[フレームワークデバイスオブジェクトの作成](creating-a-framework-device-object.md)」を参照してください。

一部のドライバーでは、プラグアンドプレイに依存しない特定の i/o 要求も処理します。 WDM ドライバーは、このような要求のターゲットとしてデバイス\_オブジェクトを作成しますが、プラグアンドプレイデバイススタックには接続しません。 同じ結果を得るために、KMDF ドライバーは[コントロールデバイスオブジェクトを作成](using-control-device-objects.md)します。 一部のフレームワークベースのドライバーは、デバイスの状態に関係なく特定の種類の i/o 要求を受信できるように、コントロールデバイスオブジェクトを使用して "sideband" i/o 機構を実装します。

## <a name="object-model"></a>オブジェクトモデル


WDF は、オブジェクトがドライバーに対して非透過的であり、ドライバーによって構成可能なコンテキスト領域を提供し、ハンドルによって参照される、一貫したオブジェクトモデルをサポートしています。 WDM オブジェクトは、ドライバーからアクセスできるシステム全体のオブジェクトであり、ポインターによって参照されます。 WDM オブジェクトを破損させるドライバーは、システム全体を破損させる可能性があります。 WDF オブジェクトを破損させるのは、ドライバーが提供するデータをフレームワークが検証するだけでなく、システム全体の問題の発生頻度も非常に低くなるため、これだけではありません。

KMDF オブジェクトの名前付け規則の詳細については、「 [WDF Architecture (アーキテクチャ](kernel-mode-driver-framework-architecture.md)の概要)」を参照してください。

フレームワークは、各オブジェクトの参照カウントを保持するため、その有効期間を制御できます。 詳細については、「[フレームワークオブジェクトのライフサイクル](framework-object-life-cycle.md)」を参照してください。

WDF オブジェクトの多くは、WDM オブジェクトに対応していますが、WDF オブジェクトは、WDM ドライバーに追加のコードを必要とする機能をサポートしています。 すべての WDF オブジェクトは、ドライバーによって定義されたオブジェクトコンテキスト領域をサポートします。これにより、ドライバーは、オブジェクトの特定のインスタンスに関連する情報をオブジェクト自体と共に格納できます。 オブジェクトは通常、状態も追跡します。 たとえば、WDFQUEUE オブジェクトは単なる i/o 要求のリストではありません。複数の種類のディスパッチ、プラグアンドプレイとの自動同期、および要求のキャンセルをサポートしています。 WDFMEMORY オブジェクトの場合、フレームワークによって管理される参照カウントによって、メモリリークやリソースの早期解放を防ぐことができます。

## <a name="object-creation"></a>オブジェクトの作成


WDF ドライバーは、すべての種類のオブジェクトを作成するために、通常のパターンに従います。

1.  オブジェクトが存在する場合は、その構成構造を初期化します。
2.  必要に応じて、オブジェクトの属性構造を初期化します。
3.  作成メソッドを呼び出してオブジェクトを作成します。

構成構造と属性構造体は、オブジェクトに関する基本的な情報と、ドライバーがそのオブジェクトを使用する方法を提供します。 すべてのオブジェクトの種類では、属性構造として[**WDF\_object\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)が使用されますが、オブジェクトの種類ごとに構成構造が異なり、オブジェクトには存在しません。 たとえば、 [**WDF\_DRIVER\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体はありますが、 **WDF\_デバイス\_config**構造体ではありません。

構成構造体は、オブジェクト固有の情報 (オブジェクトのドライバーのイベントコールバック関数など) へのポインターを保持します。 ドライバーは、この構造体にデータを読み込み、オブジェクトの作成メソッドを呼び出すときに、この構造体をフレームワークに渡します。 たとえば、 [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出すと、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数へのポインターを含む、 [**WDF\_ドライバー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体へのポインターが含まれます。

フレームワークでは、構成構造を初期化するために、WDF\_*Object*\_CONFIG\_INIT という名前の関数が定義されています。ここで、 *object*はオブジェクト型の名前を表します。 [**WDF\_オブジェクト\_属性\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)関数は、ドライバーの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体を初期化します。

## <a name="object-context-area"></a>オブジェクトコンテキスト領域


オブジェクトのすべてのインスタンスは、1つまたは複数のオブジェクトコンテキスト領域を持つことができます。 オブジェクトコンテキスト領域は、ドライバーによって割り当てられたイベントオブジェクトなど、その特定のインスタンスに関連するデータの格納領域です。 ドライバーは、オブジェクトコンテキスト領域のサイズとレイアウトを決定します。 デバイスオブジェクトの場合、オブジェクトコンテキスト領域は、WDM デバイス拡張機能に相当します。 コンテキスト領域の定義と初期化の詳細については、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

## <a name="supported-irp-types"></a>サポートされる IRP 型


WDF は、Windows Irp のサブセットをサポートします。 主な WDM IRP 型および対応する WDF イベントコールバック関数の概要については、「 [Wdm irp と WDF イベントコールバック関数](wdm-irps-and-kmdf-event-callback-functions.md)」を参照してください。

ドライバーが表に記載されている以外の Irp を受信した場合でも、KMDF に移植できます。 KMDF は、ドライバーが "未加工の" WDM Irp を受信できるメカニズムを提供しますが、他の種類の Irp にも KMDF 機能を使用します。 詳細については、「[フレームワーク以外の WDM irp の処理](handling-wdm-irps-outside-of-the-framework.md)」を参照してください。

## <a name="io-queues"></a>I/o キュー


ほとんどすべてのドライバーが i/o 要求をキューに置いています。 WDM ドライバーは、通常、次のいずれかの方法を使用します。

-   I/o 要求に対してシステムのデバイスキューを使用するには、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)関数を実装し、 [**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)と[**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出します。
-   独自の内部 i/o キューを実装するには、 **IoCsqXxx**またはその他のリスト管理関数を使用します。
-   **Kexxxdevicequeue**関数を使用して、スピンロックによって保護されているキューを初期化し、管理します。

WDF ドライバーは、i/o キューを表す WDF queue オブジェクト (WDFQUEUE) を作成します。 WDF queue オブジェクトはキャンセルセーフキューに似ていますが、追加機能が用意されています。

WDM ドライバーを WDF に移植する場合は、WDM ドライバーが使用する機構に関係なく WDF キューメカニズムを使用できます。 キューの詳細については、「[フレームワークキューオブジェクト](framework-queue-objects.md)」を参照してください。

## <a name="synchronization-and-concurrency"></a>同期と同時実行


WDF ドライバーは、WDM ドライバーでは使用できないいくつかの組み込み同期サポートの恩恵を受けます。 このサポートは、ドライバーが同時実行およびデータへの同期アクセスを無視できることを意味するわけではありませんが、WDF ドライバーは、WDM ドライバーよりもはるかに多くのロックを必要とし、同期コードが少なくてすみます。

フレームワークによって提供される同期機能の詳細については、「[同期の手法](synchronization-techniques-for-wdf-drivers.md)」を参照してください。

## <a name="driver-installation"></a>ドライバーのインストール


WDM ドライバーと同様に、KMDF および UMDF ドライバーは INF ファイルを使用してインストールされます。 ただし、WDF ドライバーのインストールには、Windows Driver Kit (WDK) に付属しているフレームワークの共同インストーラーが必要になることがあります。 共同インストーラーにより、互換性のあるバージョンのフレームワークライブラリがターゲットシステムに存在することが保証されます。 インストールの詳細については、「 [WDF ドライバーのビルドと読み込み](building-and-loading-a-kmdf-driver.md)」を参照してください。

 

 





