---
title: フィルター ドライバーでのデバイス オブジェクトの作成
description: フィルター ドライバーでのデバイス オブジェクトの作成
ms.assetid: f5a4851d-7caf-467d-9500-11f341fdf680
keywords:
- PnP WDK KMDF, フィルタードライバー
- WDK KMDF のプラグアンドプレイ、ドライバーのフィルター処理
- 電源管理 WDK KMDF, フィルタードライバー
- ドライバーのフィルター WDK KMDF
- DOs WDK KMDF のフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0752e13ee7dc6447a373ad826747afe3cab90b1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844685"
---
# <a name="creating-device-objects-in-a-filter-driver"></a>フィルター ドライバーでのデバイス オブジェクトの作成


各[フィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/filter-drivers)は、システムに存在する、サポートされている各デバイスのフレームワークデバイスオブジェクトを作成します。 これらのデバイスオブジェクトはフィルタードライバーによって作成されるため、[デバイスオブジェクトのフィルター選択] (DOs フィルター) と呼ばれます。 各フィルターは、フィルタードライバーによってデバイスが表現されます。

フィルタードライバーは関数ドライバーと同様に、 [**Wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのハンドルを受け取る[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を提供します。 ドライバーは、関数ドライバーが呼び出した同じ一連の[フレームワークデバイスオブジェクト初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-init-methods)を呼び出して、WDFDEVICE\_INIT 構造体に情報を格納できます。 関数ドライバーと同様に、フィルタードライバーは[FRAMEWORK FDO の初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#fdo-init-methods)を呼び出すこともできます。

少数のフィルタードライバーは、子ソフトウェア専用デバイスを列挙します。 このようなフィルタードライバーは、[フレームワークの PDO 初期化メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#pdo-init-methods)を呼び出すことができます。

フィルタードライバーは[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)を呼び出す必要があります。

デバイスオブジェクトを作成する最後の手順は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すことです。

 

 





