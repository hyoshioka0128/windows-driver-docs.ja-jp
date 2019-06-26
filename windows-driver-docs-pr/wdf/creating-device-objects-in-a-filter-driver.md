---
title: フィルター ドライバーでのデバイス オブジェクトの作成
description: フィルター ドライバーでのデバイス オブジェクトの作成
ms.assetid: f5a4851d-7caf-467d-9500-11f341fdf680
keywords:
- PnP WDK KMDF、フィルター ドライバー
- プラグ アンド プレイ WDK KMDF、フィルター ドライバー
- 電源管理 WDK KMDF、フィルター ドライバー
- フィルター ドライバー WDK KMDF
- DOs WDK KMDF をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4937ea8ab634ffc7a87407ab01b670d04bf37100
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377506"
---
# <a name="creating-device-objects-in-a-filter-driver"></a>フィルター ドライバーでのデバイス オブジェクトの作成


各[フィルター ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/filter-drivers)システム上に存在する、サポートされているデバイスの各フレームワーク デバイス オブジェクトを作成します。 フィルター ドライバーでは、これらのデバイス オブジェクトが作成される、ため、デバイス オブジェクトをフィルター (フィルター DOs) が呼び出されます。 デバイスのフィルター ドライバーの表現は、各フィルター操作を行います。

フィルター関数のドライバーのように、ドライバー、提供、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)を識別するハンドルを受け取るコールバック関数を[ **WDFDEVICE\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。 ドライバーは、同じセットを呼び出すことができます[framework デバイス オブジェクトの初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#device-init-methods)、WDFDEVICE で情報を格納するドライバー呼び出し関数を\_INIT 構造体。 関数のドライバーのようなフィルター ドライバーを呼び出すことも[framework FDO 初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#fdo-init-methods)します。

フィルター ドライバーの数が少ないは列挙子のソフトウェア専用デバイスです。 このようなフィルター ドライバーが呼び出せる[framework PDO 初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/#pdo-init-methods)します。

フィルター ドライバーを呼び出す必要があります[ **WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)します。

デバイス オブジェクトを作成する最後の手順を呼び出すことです。 [ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)します。

 

 





