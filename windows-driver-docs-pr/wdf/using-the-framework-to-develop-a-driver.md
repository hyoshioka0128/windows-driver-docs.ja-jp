---
title: WDF を使用したドライバーの開発
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーを開発するために使用するフレームワークオブジェクトの概要について説明します。
ms.assetid: 421b7eb8-11d3-4a37-8ae8-e2d3d216c9c7
keywords:
- カーネルモードドライバー WDK KMDF、開発手順
- KMDF WDK、開発手順
- カーネルモードドライバーフレームワーク WDK、開発手順
- フレームワークベースのドライバー WDK KMDF、開発手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b509745bced00ed952b294b862bd13c843ccde01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831967"
---
# <a name="using-wdf-to-develop-a-driver"></a>WDF を使用したドライバーの開発


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーを開発するために使用するフレームワークオブジェクトの概要について説明します。 指定されている場合を除き、同じオブジェクトを使用して、UMDF バージョン2以降のユーザーモードドライバーフレームワーク (UMDF) ドライバーを開発します。

Windows Driver framework (WDF) ドライバーは、 [**Driverentry ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)と、フレームワークベースのドライバーが使用する[windows ドライバーフレームワークオブジェクト](wdf-objects.md)によって定義される一連のイベントコールバック関数で構成されています。 コールバック関数は、フレームワークによってエクスポートされるオブジェクトメソッドを呼び出します。 Windows Driver Kit (WDK) には、ドライバーのイベントコールバック関数を実装する方法を示すサンプル WDF ドライバーが含まれています。 これらのサンプルは、 [Windows デベロッパーセンターのハードウェア](https://go.microsoft.com/fwlink/p/?linkid=256387)からダウンロードできます。 使用できるサンプルの詳細については、「 [KMDF ドライバー](sample-kmdf-drivers.md)のサンプル」および「サンプルの[UMDF ドライバー](sample-umdf-drivers.md)」を参照してください。

WDF ドライバーを作成する場合は、通常、次の操作を行います。

-   *フレームワークドライバーオブジェクト*を使用して、ドライバーを表します。

    ドライバーの[**Driverentry ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)は、 [**wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出して、ドライバーを表すフレームワークドライバーオブジェクトを作成する必要があります。 また、 **Wdfdrivercreate**メソッドは、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数も登録します。これは、プラグアンドプレイ (PnP) マネージャーが、ドライバーがサポートするデバイスの存在を報告するたびに呼び出されます。

-   *フレームワークデバイスオブジェクト*を使用して、ドライバーの PnP および電源管理をサポートします。

    すべてのドライバーは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、ドライバーがサポートする各デバイスのフレームワークデバイスオブジェクトを作成する必要があります。 デバイスは、コンピューターに接続されているハードウェアの一部である場合もあれば、ソフトウェアのみのデバイスである場合もあります。 フレームワークデバイスオブジェクトは、PnP および電源管理操作をサポートしています。また、ドライバーは、デバイスが動作状態に入ったとき、または動作状態から出たときにドライバーに通知するイベントコールバック関数を登録できます。

    フレームワークデバイスオブジェクトの詳細については、「[ドライバーでの PnP および電源管理のサポート](supporting-pnp-and-power-management-in-your-driver.md)」を参照してください。

-   *フレームワークキューオブジェクト*と*フレームワーク要求オブジェクト*を使用して、ドライバーの i/o 操作をサポートします。

    アプリケーションまたはその他のドライバーからの読み取り、書き込み、またはデバイスの i/o 制御要求を受信するすべてのドライバーは、 [**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出して、i/o キューを表すフレームワークキューオブジェクトを作成する必要があります。 通常、ドライバーは、i/o キューごとに1つまたは複数の[要求ハンドラー](request-handlers.md)を登録します。 I/o マネージャーがドライバーに i/o 要求を送信すると、フレームワークは要求のフレームワーク要求オブジェクトを作成し、要求オブジェクトを i/o キューに配置して、ドライバーの要求ハンドラーの1つを呼び出して、要求が使用可能であることをドライバーに通知します。 ドライバーは i/o 要求を取得し、要求のキューへ、完了、取り消し、または転送を行うことができます。

    フレームワークのキューオブジェクトと要求オブジェクトの使用の詳細については、「[フレームワークキューオブジェクト](framework-queue-objects.md)」と「[フレームワーク要求オブジェクト](framework-request-objects.md)」を参照してください。

-   デバイスの割り込みを処理するには、*フレームワークの interrupt オブジェクト*を使用します。

    デバイスの割り込みを処理するドライバーは、 [**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)を呼び出して、各割り込みのフレームワーク割り込みオブジェクトを作成し、コールバック関数を登録する必要があります。 これらのコールバック関数は、割り込みを有効または無効にし、割り込みの割り込みサービスルーチン (ISR) と遅延プロシージャ呼び出し (DPC) として機能します。

    フレームワークの割り込みオブジェクトの詳細については、「[ハードウェア割り込みの処理](handling-hardware-interrupts.md)」を参照してください。

-   KMDF ドライバーでは、フレームワークの*dma イネーブラーオブジェクト*と*dma トランザクションオブジェクト*を使用して、デバイスのダイレクトメモリアクセス (dma) 操作を処理できます。

    KMDF ドライバーのデバイスが DMA 操作をサポートしている場合、ドライバーは[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を呼び出して dma イネーブラーオブジェクトと[**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)を作成し、1つまたは複数の dma トランザクションオブジェクトを作成する必要があります。 DMA トランザクションオブジェクトは、デバイスハードウェアが DMA 操作を実行するようにプログラムする[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を定義します。

    DMA 操作のサポートの詳細については、「[フレームワークベースのドライバーでの Dma 操作の処理](handling-dma-operations-in-kmdf-drivers.md)」を参照してください。

-   フレームワークの i/o*ターゲットオブジェクト*を使用して、他のドライバーに i/o 要求を送信します。

    I/o 要求を他のドライバー (通常はドライバースタック内の次の下位のドライバー) に渡すために、ドライバーは i/o ターゲットオブジェクトに要求を送信します。

    I/o ターゲットオブジェクトの詳細については、「 [I/o ターゲットの使用](using-i-o-targets.md)」を参照してください。

-   KMDF ドライバーは、フレームワークの*wmi プロバイダーオブジェクト*と*wmi インスタンスオブジェクト*を使用して、Windows Management Instrumentation (wmi) 機能をサポートできます。

    ほとんどの KMDF ドライバーは WMI をサポートしている必要があり、 [**WdfWmiInstanceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/nf-wdfwmi-wdfwmiinstancecreate)を呼び出して、wmi データを送受信するコールバック関数を登録する必要があります。

    WMI の詳細については、「[フレームワークベースのドライバーでの wmi のサポート](supporting-wmi-in-kmdf-drivers.md)」を参照してください。

-   フレームワークの同期機能を使用します。

    すべてのドライバーは、マルチプロセッサの同期の問題を認識している必要があり、フレームワークが提供する[同期手法](synchronization-techniques-for-wdf-drivers.md)を使用する必要があります。

-   フレームワークによって提供される追加のオブジェクトと機能を使用します。

    このフレームワークには、ドライバーが使用できる追加のオブジェクトが用意されています。 これらのオブジェクトの詳細については、「 [WDF Support objects](wdf-support-objects.md)」を参照してください。

 

 





