---
title: 簡単な WDF ドライバーの作成
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーを作成する必要がある最小限の機能について説明します。 UMDF バージョン 2 で始まるユーザー モード ドライバー フレームワーク (UMDF) ドライバーを作成する同じ最小限の機能を必要とします。
ms.assetid: 6225b81c-e0da-473a-ba38-24846436dae7
keywords:
- カーネル モード ドライバー WDK KMDF、単純なドライバーの作成
- KMDF WDK、単純なドライバーの作成
- カーネル モード ドライバー フレームワーク WDK は、単純なドライバーの作成
- フレームワーク ベースのドライバー WDK KMDF、単純なドライバーの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8c5f470d5bb7e60af0acff5f6ac190d55947454
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386113"
---
# <a name="writing-a-simple-wdf-driver"></a>簡単な WDF ドライバーの作成


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーを作成する必要がある最小限の機能について説明します。 UMDF バージョン 2 で始まるユーザー モード ドライバー フレームワーク (UMDF) ドライバーを作成する同じ最小限の機能を必要とします。




新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。 ドライバー名は、最大長を超えている場合、ドライバーは読み込みに失敗します。

各フレームワーク ベースのドライバーから成る、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンと一連のオブジェクトに固有のイベントが発生したときにフレームワークから呼び出されるイベント コールバック関数。 たとえば、単純なフレームワーク ベースのドライバーの可能性がありますで構成されます。

-   A [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンで、ドライバーが読み込まれるときに呼び出されると呼び出し[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)します。

-   [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベント コールバック関数は、プラグ アンド プレイ (PnP) マネージャーが、ハードウェアに一致するハードウェア識別子 (ID) を使用したデバイスの検出を報告したときにフレームワークドライバーがサポートする ID です。

    ハードウェア、オペレーティング システムを使用して初めてコンピューターに接続しているデバイスのいずれかのドライバーをインストールする INF ファイルを提供することで、ドライバーをサポートする Id を指定します。 システムが INF ファイルとハードウェア Id を使用する方法の詳細については、次を参照してください。[セットアップによるドライバーの選択](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)します。

    ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数の呼び出し[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)の framework デバイス オブジェクトを作成しますデバイスが検出されました。

-   A の要求ハンドラーなど、 [ *EvtIoDefault* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) I/O マネージャーがドライバーに I/O 要求を送信するときにフレームワークから呼び出されるコールバック関数。

    I/O マネージャーは、ドライバーに、I/O 要求を送信するとき、フレームワークは I/O キューに要求を配置し、し、要求ハンドラーを呼び出すことによって、ドライバーを通知します。

    ドライバーは、ドライバーは、デバイスの I/O 要求を受信できるように、デバイスごとに少なくとも 1 つの I/O キューを作成する必要があります。 I/O キューをドライバーの呼び出しを作成する[ **WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)、framework キュー オブジェクトを作成して、デバイスの要求ハンドラーを登録します。

フレームワーク ベースのドライバーの記述方法の詳細については、次を参照してください。[ドライバーを開発するフレームワークを使用して](using-the-framework-to-develop-a-driver.md)します。

 

 





