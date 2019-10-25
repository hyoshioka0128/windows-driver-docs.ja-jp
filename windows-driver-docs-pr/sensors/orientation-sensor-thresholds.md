---
title: 方向センサーのしきい値
description: このトピックでは、方向センサーのしきい値について説明します。
ms.assetid: BC7B76C3-F6D3-48FC-AA22-A91519A0A0D8
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38888b2146b6f7ec990fc78093a55056c5d3e325
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842447"
---
# <a name="orientation-sensor-thresholds"></a>方向センサーのしきい値


このトピックでは、方向センサーのしきい値について説明します。

次の表は、向きセンサーで使用可能なしきい値を示しています。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_RotationAngle_Degrees|VT_R4|必須かどうか|10.0 f|しきい値に達するために必要な軸に対して、最小の向きの角度が変化します (度単位)。 この値は、2つの四元数の間の角度として計算する必要があります。 数学的には、次のように表されます。 2 * cos-1 (dot product (q1, q2))|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|オプション|なし|しきい値に達するために必要な x 軸に沿って加速度の最小量を増減させます (g ので測定)。|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|オプション|なし|しきい値に達するために必要な y 軸に沿った加速度の最小値の増減 (g ので測定)。|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|オプション|なし|しきい値に達するために必要な z 軸に沿って加速度の最小量を増減します (g ので測定)。|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|オプション|なし|しきい値に達するために必要な x 軸周りの角速度の最小値 (1 秒あたりの度数単位)。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|オプション|なし|しきい値に達するために必要な x 軸周りの角速度の最小値 (1 秒あたりの度数単位)。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|オプション|なし|しきい値に達するために必要な x 軸周りの角速度の最小値 (1 秒あたりの度数単位)。|

向きセンサーのドライバーは、PKEY_SensorData_RotationAngle_Degrees のしきい値に達したときに[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)を呼び出すことによって、センサークラスの拡張に対するサンプルの読み取りを報告する必要があります。

PKEY_SensorData_RotationAngle_Degrees が 0.0 f に設定されている場合、ドライバーは、すべての間隔でセンサークラス拡張にサンプルの読み取りを報告する必要があります。 このモードは*センサーサンプルストリーミング*と呼ばれています。

向きセンサードライバーは、センサークラス拡張がしきい値に関係なく[Evtsensorstart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)コールバックを呼び出すと、常に1つのサンプル読み取りを報告する必要があります。 このサンプルは、「*最初のサンプルの読み取り*」と呼ばれています。

向きセンサードライバーは、それぞれのしきい値が満たされたときに、センサークラス拡張に対するサンプル読み取りを報告する必要があります。

次に示す追加のオプションのいずれかがサポートされている場合、軸ごとの読み取りを測定します。次に、対応する軸のしきい値を公開する必要があります。
* PKEY_SensorData_LinearAccelerationX_Gs
* PKEY_SensorData_LinearAccelerationY_Gs
* PKEY_SensorData_LinearAccelerationZ_Gs
* PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond

そのため、いずれかの軸でしきい値条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出す必要があります。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

