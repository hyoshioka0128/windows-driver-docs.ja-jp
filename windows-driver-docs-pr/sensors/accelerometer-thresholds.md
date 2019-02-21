---
title: 加速度計のしきい値
description: このトピックでは、加速度計しきい値に関する情報を提供します。
ms.assetid: 7BB8B087-6CE5-4BD2-9286-350AE607B1D7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6715820e6eb21af2b4452bfa9d00b67078c9f655
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550524"
---
# <a name="accelerometer-thresholds"></a>加速度計のしきい値


このトピックでは、加速度計しきい値に関する情報を提供します。

次の表では、加速度計に利用可能なしきい値の値を示します。 型の列に示すように種類の詳細については、次を参照してください。、 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必須|0.1f|G's 単位の高速化を上げたり下げたり、しきい値に到達するために必要な軸の最小量|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必須|0.1f|G's 単位の高速化を上げたり下げたり、しきい値に到達するために必要な軸の最小量|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必須|0.1f|G's 単位の高速化を上げたり下げたり、しきい値に到達するために必要な z 軸に沿って量の最小値|

加速度計ドライバーは、呼び出すことによって、センサー クラスの拡張機能に、サンプルの読み取りを報告する必要があります[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)とき PKEY_SensorData_AccelerationX_Gs、PKEY_SensorData_AccelerationY_Gs、または PKEY_SensorData_AccelerationZ_Gs しきい値が満たされています。 各閾値は軸ごとの測定である必要があります。 軸のいずれかでしきい値の条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出すため必要があります。
PKEY_SensorData_AccelerationX_Gs、または PKEY_SensorData_AccelerationY_Gs、PKEY_SensorData_AccelerationZ_Gs を 0.0f に設定すると、ドライバーはすべて 1 つの間隔でサンプル測定値、センサー クラスの拡張機能を報告する必要があります。 このモードと呼ばれます*センサー サンプル ストリーミング*します。

加速度計ドライバーは、センサー クラスの拡張機能の呼び出し直後に、1 つの例に読み取り常に報告する必要があります、 [EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)しきい値の値に関係なくコールバック。 このサンプルと呼ばれると呼ばれる*サンプル読み取りの初期*します。

>[!NOTE]
>加速度計ドライバーでは、PKEY_SensorData_Shake データ フィールドの変更 (サポートされている) 場合、設定されているしきい値に関係なく、センサー クラスの拡張機能に読み取るサンプルも報告する必要があります。

## <a name="related-topics"></a>関連トピック

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)


