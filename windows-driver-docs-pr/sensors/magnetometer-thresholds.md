---
title: 磁力計のしきい値
description: このトピックでは、磁力計しきい値に関する情報を提供します。
ms.assetid: F245AD4C-F63C-48A7-9AEB-7414047E0627
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ecaa0ae3e678b386eb87a1be195d3bf93cc8a1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345114"
---
# <a name="magnetometer-thresholds"></a>磁力計のしきい値


このトピックでは、磁力計しきい値に関する情報を提供します。

次の表は、磁力計の使用可能なしきい値の値を示します。 型の列に示すように種類の詳細については、次を参照してください。、 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必須|5.0f|単位は microteslas、しきい値に到達するために必要な x 軸に沿った磁場の変更の最小量。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必須|5.0f|単位は microteslas、しきい値に到達するために必要な y 軸に沿った磁場の変更の最小量。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必須|5.0f|単位は microteslas、しきい値に到達するために必要な z 軸に沿って磁場の変更の最小量。|

磁力計ドライバーは、呼び出すことによって、センサー クラスの拡張機能に、サンプルの読み取りを報告する必要があります[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)とき PKEY_SensorData_ のいずれかの PKEY_SensorData_MagneticFieldStrengthX_MicroteslasMagneticFieldStrengthY_Microteslas、または PKEY_SensorData_MagneticFieldStrengthZ_Microteslas しきい値が満たされています。 各閾値は軸ごとの測定である必要があります。 軸のいずれかでしきい値の条件が満たされるたびに、ドライバーは SensorsCxSensorDataReady を呼び出すため必要があります。
PKEY_SensorData_MagneticFieldStrengthX_Microteslas、または PKEY_SensorData_MagneticFieldStrengthY_Microteslas、PKEY_SensorData_MagneticFieldStrengthZ_Microteslas を 0.0f に設定すると、ドライバーは、センサー クラスのサンプルの測定値を報告する必要があります。すべての間隔で拡張機能。 このモードと呼ばれます*センサー サンプル ストリーミング*します。

磁力計ドライバーは、センサー クラスの拡張機能の呼び出し直後に、1 つの例に読み取り常に報告する必要があります、 [EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)しきい値の値に関係なくコールバック。 このサンプルと呼ばれると呼ばれる*サンプル読み取りの初期*します。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 


