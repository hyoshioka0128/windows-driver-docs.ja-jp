---
title: 方向センサーのしきい値
description: このトピックでは、センサーのしきい値については、印刷の向きを示します。
ms.assetid: BC7B76C3-F6D3-48FC-AA22-A91519A0A0D8
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a6c2bdd28e3ad84ffd6cfe166b0b216786f79c93
ms.sourcegitcommit: 85b989c149403210f2c7b892e045d037580432e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2019
ms.locfileid: "66825048"
---
# <a name="orientation-sensor-thresholds"></a>方向センサーのしきい値


このトピックでは、センサーのしきい値については、印刷の向きを示します。

次の表では、方向センサーの使用可能なしきい値の値を示します。 型の列に示すように種類の詳細については、次を参照してください。、 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_RotationAngle_Degrees|VT_R4|必須|10.0f|向きの角度が度数法で、しきい値に到達するために必要なすべての軸を中心変更の最小量。 この値は、2 つの四元数の間の角度として計算する必要があります。 数学的に、これで表されます。2*cos-1 (dot product(q1, q2))|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|省略可能|なし|G's 単位の高速化を上げたり下げたり、しきい値に到達するために必要な軸の最小量|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|省略可能|なし|G's 単位の高速化を上げたり下げたり、しきい値に到達するために必要な軸の最小量|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|省略可能|なし|G's 単位の高速化を上げたり下げたり、しきい値に到達するために必要な z 軸に沿って量の最小値|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|省略可能|なし|1 秒あたりの度数法で、しきい値に到達するために必要な軸角度の速度の変更の最小量。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|省略可能|なし|1 秒あたりの度数法で、しきい値に到達するために必要な軸角度の速度の変更の最小量。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|省略可能|なし|1 秒あたりの度数法で、しきい値に到達するために必要な軸角度の速度の変更の最小量。|

方向センサー ドライバーは、読み取りは呼び出すことによって、センサー クラスの拡張機能サンプルを報告する必要があります[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready) PKEY_SensorData_RotationAngle_Degrees しきい値が満たされたときにします。

PKEY_SensorData_RotationAngle_Degrees が 0.0f に設定されている場合、ドライバーは、すべての間隔でセンサー クラスの拡張機能のサンプルの測定値を報告する必要があります。 このモードと呼ばれます*センサー サンプル ストリーミング*します。

方向センサー ドライバーは、センサー クラスの拡張機能の呼び出し直後に、1 つの例に読み取り常に報告する必要があります、 [EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)しきい値の値に関係なくコールバック。 このサンプルと呼ばれると呼ばれる*サンプル読み取りの初期*します。

方向センサー ドライバーには、それぞれのしきい値が満たされたときに、センサー クラスの拡張機能への読み込み中のサンプルをレポートする必要があります。

ドライバーをサポートし、軸ごとの測定値を測定する、省略可能な次の追加のデータ フィールドのいずれかを対応する軸のしきい値が公開する必要があります。
* PKEY_SensorData_LinearAccelerationX_Gs
* PKEY_SensorData_LinearAccelerationY_Gs
* PKEY_SensorData_LinearAccelerationZ_Gs
* PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond
* PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond

軸のいずれかでしきい値の条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出すため必要があります。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

