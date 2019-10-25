---
title: ジャイロスコープのしきい値
description: このトピックでは、ジャイロスコープしきい値について説明します。
ms.assetid: 68B11108-CA1A-4A49-BC44-4E9FE09955A9
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 09def43c8fa88f6b8ae882df5091aebce5889d77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841684"
---
# <a name="gyroscope-thresholds"></a>ジャイロスコープのしきい値


このトピックでは、ジャイロスコープしきい値について説明します。

次の表は、ジャイロスコープの既定のしきい値を示しています。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_AngularVelocityX_DegreesPerSecond|VT_R4|必須かどうか|0.1 f|しきい値に達するために必要な x 軸周りの角速度の最小値 (1 秒あたりの度数単位)。|
|PKEY_SensorData_AngularVelocityY_DegreesPerSecond|VT_R4|必須かどうか|0.1 f|しきい値に達するために必要な y 軸周辺の角速度の最小値 (1 秒あたりの度数単位)。|
|PKEY_SensorData_AngularVelocityZ_DegreesPerSecond|VT_R4|必須かどうか|0.1 f|しきい値に達するために z 軸を中心とする角速度の最小値 (1 秒あたりの度数単位)。|

ジャイロスコープドライバーは、PKEY_SensorData_AngularVelocityX_DegreesPerSecond、PKEY_SensorData_AngularVelocityY_DegreesPerSecond、または PKEY_ のいずれかで[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)を呼び出すことによって、センサークラス拡張に対するサンプルの読み取りを報告する必要があります。SensorData_AngularVelocityZ_DegreesPerSecond のしきい値を満たしています。 各しきい値は、軸ごとに測定する必要があります。 そのため、いずれかの軸でしきい値条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出す必要があります。
PKEY_SensorData_AngularVelocityX_DegreesPerSecond、PKEY_SensorData_AngularVelocityY_DegreesPerSecond、または PKEY_SensorData_AngularVelocityZ_DegreesPerSecond が 0.0 f に設定されている場合、ドライバーはサンプルの読み取りをセンサークラスに報告する必要があります。各間隔の拡張機能。 このモードは*センサーサンプルストリーミング*と呼ばれています。

センサークラス拡張がしきい値に関係なく[Evtsensorstart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)コールバックを呼び出すと、ジャイロスコープドライバーは常に1つのサンプル読み取りを報告する必要があります。 このサンプルは、「最初のサンプルの読み取り」と呼ばれています。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)







