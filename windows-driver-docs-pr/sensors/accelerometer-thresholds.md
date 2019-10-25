---
title: 加速度計のしきい値
description: このトピックでは、加速度計しきい値について説明します。
ms.assetid: 7BB8B087-6CE5-4BD2-9286-350AE607B1D7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2de9645ac133d999f1a368643a1a15d7f23f43d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824292"
---
# <a name="accelerometer-thresholds"></a>加速度計のしきい値


このトピックでは、加速度計しきい値について説明します。

次の表に、加速度計で使用可能なしきい値の一覧を示します。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必須かどうか|0.1 f|しきい値に達するために必要な x 軸に沿って加速度の最小量を増減させます (g ので測定)。|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必須かどうか|0.1 f|しきい値に達するために必要な y 軸に沿った加速度の最小値の増減 (g ので測定)。|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必須かどうか|0.1 f|しきい値に達するために必要な z 軸に沿って加速度の最小量を増減します (g ので測定)。|

加速度計ドライバーは、PKEY_SensorData_AccelerationX_Gs、PKEY_SensorData_AccelerationY_Gs、または PKEY_SensorData_AccelerationZ_Gs のいずれかで[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)を呼び出すことによって、センサークラス拡張に対するサンプルの読み取りを報告する必要があります。しきい値が満たされています。 各しきい値は、軸ごとに測定する必要があります。 そのため、いずれかの軸でしきい値条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出す必要があります。
PKEY_SensorData_AccelerationX_Gs、PKEY_SensorData_AccelerationY_Gs、または PKEY_SensorData_AccelerationZ_Gs が 0.0 f に設定されている場合、ドライバーは、1回の間隔でセンサークラス拡張にサンプルの読み取りを報告する必要があります。 このモードは*センサーサンプルストリーミング*と呼ばれています。

センサークラス拡張がしきい値に関係なく[Evtsensorstart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)コールバックを呼び出すと、加速度計ドライバーは常に1つのサンプル読み取りを報告する必要があります。 このサンプルは、「*最初のサンプルの読み取り*」と呼ばれています。

>[!NOTE]
>また、加速度計ドライバーは、設定されているしきい値に関係なく、PKEY_SensorData_Shake データフィールドが (サポートされている場合) 変更されたときにセンサークラスの拡張機能に対する読み取りサンプルを報告する必要があります。

## <a name="related-topics"></a>関連トピック

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)


