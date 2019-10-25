---
title: 簡単な WDF ドライバーの作成
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーを記述するために必要な最小限の機能について説明します。 UMDF バージョン2以降では、ユーザーモードドライバーフレームワーク (UMDF) ドライバーを記述するのに必要な最小限の機能が必要です。
ms.assetid: 6225b81c-e0da-473a-ba38-24846436dae7
keywords:
- カーネルモードドライバー WDK KMDF、シンプルなドライバーの作成
- KMDF WDK、シンプルなドライバーの作成
- カーネルモードドライバーフレームワーク WDK、単純なドライバーの作成
- フレームワークベースのドライバー WDK KMDF、シンプルなドライバーの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeacb11bdfc4cf2033b6177779ba2802ecd28f6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823490"
---
# <a name="writing-a-simple-wdf-driver"></a>簡単な WDF ドライバーの作成


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーを記述するために必要な最小限の機能について説明します。 UMDF バージョン2以降では、ユーザーモードドライバーフレームワーク (UMDF) ドライバーを記述するのに必要な最小限の機能が必要です。




新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。 ドライバー名が最大長を超えていると、ドライバーの読み込みに失敗します。

各フレームワークベースのドライバーは、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンと、オブジェクト固有のイベントが発生したときにフレームワークが呼び出す一連のイベントコールバック関数で構成されます。 たとえば、単純なフレームワークベースのドライバーは次のように構成されます。

-   [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチン。ドライバーが読み込まれ、 [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出すときに呼び出されます。

-   [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバック関数。この関数は、プラグアンドプレイ (PnP) マネージャーが、ドライバーがサポートするハードウェア id と一致するデバイスの検出をハードウェア識別子 (id) で報告したときに呼び出します。

    ドライバーがサポートするハードウェア Id を指定するには、INF ファイルを提供します。このファイルは、デバイスの1つがコンピューターに初めて接続されたときに、オペレーティングシステムがドライバーをインストールするために使用します。 システムで INF ファイルとハードウェア Id を使用する方法の詳細については、「[セットアップでドライバーを選択する方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)」を参照してください。

    ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、検出されたデバイスのフレームワークデバイスオブジェクトを作成します。

-   I/o マネージャーがドライバーに i/o 要求を送信したときにフレームワークが呼び出す、 [*Evtiodefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)コールバック関数などの要求ハンドラー。

    I/o マネージャーがドライバーに i/o 要求を送信すると、フレームワークは要求を i/o キューに配置し、要求ハンドラーを呼び出してドライバーに通知します。

    ドライバーは、デバイスの i/o 要求を受信できるように、デバイスごとに1つ以上の i/o キューを作成する必要があります。 I/o キューを作成するために、ドライバーは[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出します。これにより、フレームワークキューオブジェクトが作成され、デバイスの要求ハンドラーが登録されます。

フレームワークベースのドライバーの記述の詳細については、「フレームワークを使用した[ドライバーの開発](using-the-framework-to-develop-a-driver.md)」を参照してください。

 

 





