---
title: センサー DDSI コールバック
description: センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) 関数では、センサー ドライバーは、クラスの拡張機能との対話を使用してインターフェイスを表します。
ms.assetid: 3DB30155-8DBE-4AE9-A0CC-8089DC255E32
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6201e6ab3671aad57b0df150c075eef11b0075e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368882"
---
# <a name="sensor-ddsi-callbacks"></a>センサー DDSI コールバック

センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) 関数では、センサー ドライバーは、クラスの拡張機能との対話を使用してインターフェイスを表します。 これらのコールバックはセンサー ドライバーによって実装され、クラスの拡張機能によって呼び出されます。 詳細については、これらのコールバックでを見つけることができます、 [_SENSOR_CONTROLLER_CONFIG 構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)します。

## <a name="callbacks"></a>コールバック

|トピック|説明|
|---|---|
|EvtSensorDisableWake|センサーのスリープ解除を無効にするコールバック。 |
|EvtSensorEnableWake|センサーのスリープ解除を有効にするコールバック。|
|EvtSensorStartStateChangeNotification|状態変更の通知を開始するために使用します。|
|EvtSensorStopStateChangeNotification|状態変更の通知を停止するために使用します。|
|EvtSensorStart|このコールバック関数は、ドライバーで指定された既定のプロパティに基づいて、センサーを開始またはクラスの拡張機能によって設定されたプロパティ。|
|EvtSensorStop|このコールバック関数では、センサーが停止します。|
|EvtSensorGetSupportedDataFields|このコールバック関数では、指定されたセンサーでサポートされているデータ フィールドの一覧を返します。|
|EvtSensorGetProperties|このコールバック関数では、特定のセンサーのプロパティを返します。|
|EvtSensorGetDataFieldProperties|このコールバック関数では、センサーに関連付けられている特定のデータ フィールドのプロパティを返します。|
|EvtSensorGetDataInterval|このコールバック関数では、指定したセンサー データの間隔を返します。|
|EvtSensorSetDataInterval|このコールバック関数では、指定したセンサー データの間隔を設定します。|
|EvtSensorGetDataThresholds|このコールバック関数では、センサーに関連付けられているしきい値を返します。|
|EvtSensorSetDataThresholds|このコールバック関数では、1 つまたは複数のデータ フィールドに関連付けられたセンサーのしきい値を設定します。|
|EvtSensorDeviceIoControl|このコールバック関数は、クラス拡張の外部で Ioctl を処理します。|
|EvtSensorSetBatchLatency|このコールバック関数では、指定したセンサーのバッチの待機時間を設定します。|

