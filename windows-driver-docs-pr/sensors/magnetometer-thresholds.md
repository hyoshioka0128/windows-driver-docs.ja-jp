---
title: 磁力計のしきい値
description: このトピックでは、磁力計しきい値について説明します。
ms.assetid: F245AD4C-F63C-48A7-9AEB-7414047E0627
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: db31b3becb25872b07319542521183981b0afa1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842451"
---
# <a name="magnetometer-thresholds"></a>磁力計のしきい値


このトピックでは、磁力計しきい値について説明します。

次の表は、磁力計で使用可能なしきい値を示しています。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必須かどうか|5.0 f|しきい値に達するために必要な x 軸に沿った磁気フィールド変更の最小量 (マイクロ tesラスベガスで測定)。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必須かどうか|5.0 f|しきい値に達するために必要な、y 軸に沿った磁気フィールド変更の最小量 (マイクロ tesラスベガスで測定)。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必須かどうか|5.0 f|しきい値に達するために必要な、z 軸に沿った磁気フィールド変更の最小量 (マイクロ tesラスベガスで測定)。|

磁力計ドライバーは、PKEY_SensorData_MagneticFieldStrengthX_Microteslas、PKEY_SensorData_MagneticFieldStrengthY_Microteslas、またはのいずれかで[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)を呼び出すことによって、センサークラス拡張に対するサンプルの読み取りを報告する必要があります。PKEY_SensorData_MagneticFieldStrengthZ_Microteslas のしきい値を満たしています。 各しきい値は、軸ごとに測定する必要があります。 そのため、いずれかの軸でしきい値条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出す必要があります。
PKEY_SensorData_MagneticFieldStrengthX_Microteslas、PKEY_SensorData_MagneticFieldStrengthY_Microteslas、または PKEY_SensorData_MagneticFieldStrengthZ_Microteslas が 0.0 f に設定されている場合、ドライバーはサンプルの読み取りをセンサークラスに報告する必要があります。各間隔の拡張機能。 このモードは*センサーサンプルストリーミング*と呼ばれています。

センサークラス拡張がしきい値に関係なく[Evtsensorstart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)コールバックを呼び出すと、磁力計ドライバーは常に1つのサンプル読み取りを報告する必要があります。 このサンプルは、「*最初のサンプルの読み取り*」と呼ばれています。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 


