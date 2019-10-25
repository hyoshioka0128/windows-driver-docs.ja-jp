---
title: センサー DDSI コールバック
description: センサーデバイスドライバーソフトウェアインターフェイス (DDSI) 関数は、センサードライバーがクラス拡張との対話に使用するインターフェイスを表します。
ms.assetid: 3DB30155-8DBE-4AE9-A0CC-8089DC255E32
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae44c084db096b80be45790ccac74c1c4cb661ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845501"
---
# <a name="sensor-ddsi-callbacks"></a>センサー DDSI コールバック

センサーデバイスドライバーソフトウェアインターフェイス (DDSI) 関数は、センサードライバーがクラス拡張との対話に使用するインターフェイスを表します。 これらのコールバックはセンサードライバーによって実装され、クラス拡張によって呼び出されます。 これらのコールバックの詳細については、[構成の構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)を参照してください。

## <a name="callbacks"></a>関数

|トピック|説明|
|---|---|
|EvtSensorDisableWake|センサーの wake を無効にするコールバック。 |
|EvtSensorEnableWake|センサーのスリープ解除を有効にするコールバック。|
|EvtSensorStartStateChangeNotification|状態変更通知を開始するために使用します。|
|EvtSensorStopStateChangeNotification|状態変更通知を停止するために使用します。|
|EvtSensorStart|このコールバック関数は、ドライバーによって指定された既定のプロパティまたはクラス拡張によって設定されたプロパティに基づいて、センサーを開始します。|
|EvtSensorStop|このコールバック関数はセンサーを停止します。|
|EvtSensorGetSupportedDataFields|このコールバック関数は、指定されたセンサーによってサポートされるデータフィールドの一覧を返します。|
|EvtSensorGetProperties|このコールバック関数は、特定のセンサーのプロパティを返します。|
|EvtSensorGetDataFieldProperties|このコールバック関数は、センサーに関連付けられている特定のデータフィールドのプロパティを返します。|
|EvtSensorGetDataInterval|このコールバック関数は、指定されたセンサーのデータ間隔を返します。|
|EvtSensorSetDataInterval|このコールバック関数は、指定されたセンサーのデータ間隔を設定します。|
|EvtSensorGetDataThresholds 値|このコールバック関数は、センサーに関連付けられているしきい値を返します。|
|EvtSensorSetDataThresholds 値|このコールバック関数は、センサーに関連付けられている1つ以上のデータフィールドのしきい値を設定します。|
|EvtSensorDeviceIoControl|このコールバック関数は、クラス拡張外の Ioctl を処理します。|
|EvtSensorSetBatchLatency|このコールバック関数は、指定されたセンサーのバッチ待機時間を設定します。|

