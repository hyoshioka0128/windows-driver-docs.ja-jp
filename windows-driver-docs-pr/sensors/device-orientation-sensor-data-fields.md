---
title: 方向センサーのデータ フィールド
description: このトピックでは、方向センサーに固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: 4B1FA56E-6956-4BC9-B929-3D78EF933057
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 80a84e47de6a5e48d76e34ea413d6b03e9f71ffc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537950"
---
# <a name="orientation-sensor-data-fields"></a>方向センサーのデータ フィールド


このトピックでは、方向センサーに固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、次を参照してください。、 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明/コメント|
|---|---|---|---|
|PKEY_SensorData_QuaternionW|VT_R4|必須|回転の軸のベクターの (複素数の虚数部の部分) ではなく実際の係数。|
|PKEY_SensorData_QuaternionX|VT_R4|必須|回転の軸のベクターの X 成分。|
|PKEY_SensorData_QuaternionY|VT_R4|必須|回転の軸のベクターの Y 成分。|
|PKEY_SensorData_QuaternionZ|VT_R4|必須|回転の軸のベクトルの Z 成分。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必須|磁力計センサーの精度。 有効な値の詳細については、次を参照してください。 [MAGNETOMETER_ACCURACY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-magnetometer_accuracy)します。|
|PKEY_SensorData_DeclinationAngle_Degrees|VT_R4|省略可能|磁気拒否角度が地球の方位は磁北から真北を推測するために使用します。 サポートされていない場合、クラス拡張はこの値を計算します。|
|PKEY_SensorData_LinearAccelerationX_Gs|VT_R4|省略可能|G's で線形の加速を x 軸|
|PKEY_SensorData_LinearAccelerationY_Gs|VT_R4|省略可能|G's で線形の加速を y 軸|
|PKEY_SensorData_LinearAccelerationZ_Gs|VT_R4|省略可能|G's で線形の加速を z 軸|
|PKEY_SensorData_CorrectedAngularVelocityX_DegreesPerSecond|VT_R4|省略可能|Gyrometric x 軸の速度 (1 秒あたりの角度)。|
|PKEY_SensorData_CorrectedAngularVelocityY_DegreesPerSecond|VT_R4|省略可能|Gyrometric y 軸の速度 (1 秒あたりの角度)。|
|PKEY_SensorData_CorrectedAngularVelocityZ_DegreesPerSecond|VT_R4|省略可能|Gyrometric z 軸の速度 (1 秒あたりの角度)。|


## <a name="related-topics"></a>関連トピック


[MSDN PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)






