---
title: ジャイロスコープしきい値
description: このトピックでは、ジャイロスコープしきい値に関する情報を提供します。
ms.assetid: 68B11108-CA1A-4A49-BC44-4E9FE09955A9
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: dadbee3a04b7d89e7d2f33e1cb7e7ce26ca86b59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553382"
---
# <a name="gyroscope-thresholds"></a>ジャイロスコープしきい値


このトピックでは、ジャイロスコープしきい値に関する情報を提供します。

次の表は、既定のしきい値をジャイロスコープなどがあります。 型の列に示すように種類の詳細については、、 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)を参照してください。

|プロパティのキー|種類|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_AngularVelocityX_DegreesPerSecond|VT_R4|必須|0.1f|1 秒あたりの度数法で、しきい値に到達するために必要な軸角度の速度の変更の最小量。|
|PKEY_SensorData_AngularVelocityY_DegreesPerSecond|VT_R4|必須|0.1f|1 秒あたりの度数法で、しきい値に到達するために必要な y 軸の周りの角度の速度の変更の最小量。|
|PKEY_SensorData_AngularVelocityZ_DegreesPerSecond|VT_R4|必須|0.1f|1 秒あたりの度数法で、しきい値に到達するために必要な z 軸角度の速度の変更の最小量。|

ジャイロスコープ ドライバーは、呼び出すことでセンサー クラスの拡張機能に、サンプルの読み取りを報告する必要があります[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)とき PKEY_SensorData_AngularVelocityY_ のいずれかの PKEY_SensorData_AngularVelocityX_DegreesPerSecondDegreesPerSecond、または PKEY_SensorData_AngularVelocityZ_DegreesPerSecond しきい値が満たされています。 各閾値は軸ごとの測定である必要があります。 軸のいずれかでしきい値の条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出すため必要があります。
PKEY_SensorData_AngularVelocityX_DegreesPerSecond、または PKEY_SensorData_AngularVelocityY_DegreesPerSecond、PKEY_SensorData_AngularVelocityZ_DegreesPerSecond を 0.0f に設定すると、ドライバーは、センサー クラスのサンプルの測定値を報告する必要があります。すべての間隔で拡張機能。 このモードと呼ばれます*センサー サンプル ストリーミング*します。

ジャイロスコープ ドライバーは、センサー クラスの拡張機能の呼び出し直後に、1 つの例に読み取り常に報告する必要があります、 [EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)しきい値の値に関係なくコールバック。 このサンプルは、サンプルの初期読み込みと呼ばれると呼ばれます。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)







