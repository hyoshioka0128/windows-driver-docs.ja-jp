---
title: 方向センサーのデータフィールド
description: このトピックでは、向きセンサーに固有のデータフィールドについて説明します。
ms.assetid: 4B1FA56E-6956-4BC9-B929-3D78EF933057
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 287a1a5fbaad25c572c9f54fdbc3999abbc26164
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841692"
---
# <a name="orientation-sensor-data-fields"></a>方向センサーのデータフィールド


このトピックでは、向きセンサーに固有のデータフィールドについて説明します。

次の表は、データフィールドを示しています。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|種類|必須/省略可能|説明/コメント|
|---|---|---|---|
|PKEY_SensorData_QuaternionW|VT_R4|必須|回転軸ベクトルの複素数の虚数部ではなく、実数係数。|
|PKEY_SensorData_QuaternionX|VT_R4|必須|回転軸ベクトルの X 成分。|
|PKEY_SensorData_QuaternionY|VT_R4|必須|回転軸ベクトルの Y 成分。|
|PKEY_SensorData_QuaternionZ|VT_R4|必須|回転軸ベクトルの Z 成分。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必須|磁力計センサーの精度。 有効な値の詳細については、「 [MAGNETOMETER_ACCURACY](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-magnetometer_accuracy)」を参照してください。|
|PKEY_SensorData_DeclinationAngle_Degrees|VT_R4|省略可能|地球の磁方位から真の北を推測するために使用される磁拒否角度。 サポートされていない場合は、クラス拡張によってこの値が計算されます。|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|省略可能|X 軸の線形加速度 (g の)|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|省略可能|G の Y 軸の線形加速度|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|省略可能|Z 軸の線形加速度 (g)|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|省略可能|Gyrometric X 軸速度 (°/秒)。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|省略可能|Gyrometric Y 軸速度 (°/秒)。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|省略可能|Gyrometric Z 軸速度 (°/秒)。|


## <a name="related-topics"></a>関連トピック


[MSDN PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)






