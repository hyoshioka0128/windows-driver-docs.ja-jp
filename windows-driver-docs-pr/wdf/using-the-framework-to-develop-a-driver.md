---
title: WDF を使用してドライバーを開発するには
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーの開発に使用するフレームワーク オブジェクトの概要を説明します。
ms.assetid: 421b7eb8-11d3-4a37-8ae8-e2d3d216c9c7
keywords:
- カーネル モード ドライバー WDK KMDF、開発手順
- KMDF WDK、開発手順
- カーネル モード ドライバー フレームワーク WDK の開発手順
- フレームワーク ベースのドライバー WDK KMDF、開発手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e27575d44a27f611034e3c70b9b75e9d1160a14d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530545"
---
# <a name="using-wdf-to-develop-a-driver"></a>WDF を使用してドライバーを開発するには


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーの開発に使用するフレームワーク オブジェクトの概要を説明します。 場所が示されるように、除く以降 UMDF バージョン 2 では、ユーザー モード ドライバー フレームワーク (UMDF) ドライバーを開発するのに同じオブジェクトを使用します。

Windows Driver Frameworks (WDF) ドライバーから成る、 [ **DriverEntry ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff540807)と一連のイベントのコールバック関数で定義されている、 [Windows Driver Framework オブジェクト](wdf-objects.md)framework ベースのドライバーが使用されます。 コールバック関数では、フレームワークをエクスポートするオブジェクトのメソッドを呼び出します。 Windows Driver Kit (WDK) には、ドライバーのイベントのコールバック関数を実装する方法を示すサンプル WDF ドライバーが含まれています。 これらのサンプルをダウンロードすることができます、 [Windows デベロッパー センター - ハードウェア](https://go.microsoft.com/fwlink/p/?linkid=256387)します。 どのようなサンプルが使用可能な方法の詳細については、[サンプル KMDF ドライバー](sample-kmdf-drivers.md)と[サンプル UMDF ドライバー](sample-umdf-drivers.md)を参照してください。

WDF のドライバーを作成するときに通常、以下の。

-   使用して、 *framework ドライバー オブジェクト*ドライバーを表すため。

    ドライバーの[ **DriverEntry ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff540807)呼び出す必要があります[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)を表すフレームワーク ドライバー オブジェクトを作成しますドライバー。 **WdfDriverCreate**メソッドには、ドライバーの登録も[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数は、各フレームワークの時間をプラグ アンド プレイ (PnP)マネージャーは、ドライバーがサポートするデバイスの存在をレポートします。

-   使用*framework デバイス オブジェクト*ドライバー、PnP や電源管理をサポートするためにします。

    すべてのドライバーを呼び出す必要があります[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)各デバイス ドライバーをサポートするフレームワーク デバイス オブジェクトを作成します。 デバイスは、コンピューターに接続されているハードウェアを指定できますか、ソフトウェア専用デバイスであることができます。 PnP デバイス オブジェクトのフレームワークをサポートし、電源管理操作とドライバーは、デバイスに入るか出るの稼働状態になったときに、ドライバーを通知するイベントのコールバック関数を登録できます。

    Framework デバイス オブジェクトの詳細については、[PnP をサポートしていると、ドライバーでの電源管理](supporting-pnp-and-power-management-in-your-driver.md)を参照してください。

-   使用*framework キュー オブジェクト*と*framework 要求オブジェクト*ドライバー、I/O 操作をサポートするためにします。

    読み取り、書き込み、またはデバイスの I/O を受信するすべてのドライバーがアプリケーションからの要求を制御したり、他のドライバーを呼び出す必要があります[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)フレームワークの I/O キューを表すキュー オブジェクトを作成します。 通常、ドライバーは、1 つまたは複数を登録[要求ハンドラー](request-handlers.md) I/O キューごとにします。 I/O マネージャーでは、ドライバー、I/O 要求を送信するときにフレームワークは要求に対するフレームワークの要求オブジェクトを作成、要求オブジェクトを I/O キューに配置し、要求が使用できることをドライバーに通知するために、ドライバーの要求ハンドラーの 1 つを呼び出します。 ドライバーは、I/O 要求を取得およびことができますをもう一度キュー、完了、キャンセル、または要求を転送します。

    詳細については、フレームワークのキュー オブジェクトとの要求オブジェクトを使用して、[Framework キュー オブジェクト](framework-queue-objects.md)と[Framework 要求オブジェクト](framework-request-objects.md)を参照してください。

-   使用*framework 割り込みオブジェクト*デバイス割り込みを処理します。

    デバイスの割り込みを処理するドライバーを呼び出す必要があります[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)を各割り込みの framework 割り込みオブジェクトを作成し、コールバック関数を登録します。 これらのコールバック関数を有効にして、割り込みを無効にする割り込みサービス ルーチン (ISR) として機能し、割り込みのプロシージャ呼び出し (DPC) の遅延。

    フレームワークの割り込みのオブジェクトの詳細については、[ハードウェアの割り込み処理](handling-hardware-interrupts.md)を参照してください。

-   KMDF ドライバーは、framework を使用して*DMA イネーブラー オブジェクト*と*DMA トランザクション オブジェクト*デバイスのダイレクト メモリ アクセス (DMA) 操作を処理します。

    KMDF ドライバーのデバイスでは、DMA 操作をサポートする場合、ドライバーを呼び出す必要があります[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983) DMA イネーブラー オブジェクトを作成して[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027) 1 つまたは複数の DMA トランザクション オブジェクトを作成します。 DMA のトランザクション オブジェクトを定義、 [ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816) DMA 操作を実行するデバイスのハードウェアをプログラムするコールバック関数。

    DMA 操作のサポートの詳細については、[Framework ベースのドライバーの DMA 操作を処理](handling-dma-operations-in-kmdf-drivers.md)を参照してください。

-   使用して、フレームワークの*I/O ターゲット オブジェクト*I/O 要求を他のドライバーに送信します。

    I/O 要求を他のドライバー (通常、[次へ] 下位のドライバーはドライバー スタックで) で渡すには、ドライバーは、I/O のターゲット オブジェクトに、要求を送信します。

    I/O ターゲット オブジェクトの詳細については、[を使用して I/O ターゲット](using-i-o-targets.md)を参照してください。

-   フレームワークのことができます、KMDF ドライバーを使用して、 *WMI プロバイダー オブジェクト*と*WMI インスタンス オブジェクト*Windows Management Instrumentation (WMI) の機能をサポートします。

    KMDF ドライバーのほとんどは、WMI をサポートする必要があり、呼び出す必要があります[ **WdfWmiInstanceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551178)送信または WMI データを受信するコールバック関数を登録します。

    WMI の詳細については、[Framework ベースのドライバーでサポートしている WMI](supporting-wmi-in-kmdf-drivers.md)を参照してください。

-   フレームワークの同期機能を使用します。

    すべてのドライバーのマルチプロセッサ同期の問題に注意する必要があり、使用する必要があります[同期手法](synchronization-techniques-for-wdf-drivers.md)フレームワークを提供します。

-   その他のオブジェクトとフレームワークを提供する機能を使用します。

    フレームワークは、ドライバーを使用して追加のオブジェクトを提供します。 これらのオブジェクトの詳細については、[WDF サポート オブジェクト](wdf-support-objects.md)を参照してください。

 

 





