---
title: 光センサーのしきい値
description: このトピックでは、光センサーのしきい値に関する情報を提供します。
ms.assetid: A120601A-A5CE-4778-94A9-97E71B721E9B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f87faf112f72635362704fe06e3ce5b82f38745f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549421"
---
# <a name="light-sensor-thresholds"></a>光センサーのしきい値


このトピックでは、光センサーのしきい値に関する情報を提供します。

次の表では、光センサーのドライバーの既定のしきい値を示します。 光センサーの既定の間隔は、10 Hz です。 型の列に示すように種類の詳細については、、 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)を参照してください。

|プロパティのキー|種類|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_LightLevel_Lux|VT_R4|必須|0.25f|最小量のしきい値に到達するために必要な照度の変更は、lux に占める割合で測定されます。 0.25f の値は、照度で 25% の変更を意味します。|
|PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference|VT_R4|省略可能|1.0 f|最小量のしきい値に到達するために必要な照度の変更は、lux で測定されます。 1.0 f の値は、1 lux 照度で変更します。 <br>__注:__ このしきい値の実装は強くお勧めしますポータブル デバイスで低のアンビエント ライト環境でバッテリ電力消費の削減に役立ちます。|
|PKEY_SensorData_LightChromaticityX|VT_R4|色がサポートされているかどうかに必要です。 それ以外の場合 (省略可能)|0.01f|絶対の差で表される、しきい値に到達するために必要な色の座標 x CIE 1931 の変更の最小量。|
|PKEY_SensorData_LightChromaticityY|VT_R4|色がサポートされているかどうかに必要です。 それ以外の場合 (省略可能)|0.01f|絶対の差で表される、しきい値に到達するために必要な CIE 1931 y 色座標の変更の最小量。|
|PKEY_SensorData_LightTemperature_Kelvins|VT_R4|色がサポートされているかどうかに必要です。 それ以外の場合 (省略可能)|50.0 f|ケルビンで、しきい値に到達するために必要な光、温度の変更の最小量が測定されます。|

光センサーは、新しいデータのサンプルを報告する必要があります*LUX 値が変更された場合にのみ*します。 レポート モデルで光センサーは報告されていないこと新しいデータ サンプル繰り返し、完全に暗いである場合に、この推奨は、ゼロ (0) LUX 環境。

環境光センサー ドライバーが呼び出すことでセンサー クラスの拡張機能に、サンプルの読み取りを報告する必要があります PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が指定されていない場合[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready)とき PKEY_SensorData_LightLevel_Lux しきい値が満たされるとします。 PKEY_SensorData_LightLevel_Lux しきい値は、lux の差の割合として表されます。 たとえば、0.25f にこのしきい値を設定し、センサー クラスの拡張機能に報告された前回のサンプルは、40 lux が場合、報告されることを次のサンプルは 30 lux より低いまたはあります (40 の 25%) +/-50 lux より大きい。
PKEY_SensorData_LightLevel_Lux に加えて PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が提供される場合は、環境光センサーする必要がありますレポートのサンプル読み取りセンサー クラスの拡張機能に場合__両方__しきい値が満たされています。 0.25 (つまり、25%) 4.0 lux を PKEY_SensorData_LightLevel_Lux PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が設定されている場合を設定する例。読み取り、最後のサンプルの値が 4 lux センサー クラスの拡張機能に報告された場合、最も制限の厳しいしきい値 PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference。 そのため、0 lux または 8 lux 報告されることを次のサンプルの読み取りになります。
比較的、4.0 lux を PKEY_SensorData_LightLevel_Lux PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が設定されている場合に設定されている 0.25 (つまり、25%)読み取りが前回のサンプルの値は 40 lux センサー クラスの拡張機能に報告された、最も制限の厳しいしきい値は PKEY_SensorData_LightLevel_Lux。 この場合は、30 lux または 50 lux 報告されることを次のサンプルの読み取りになります。
PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference は PKEY_SensorData_LightLevel_Lux せずは設定しないでください。

センサー ドライバーが一番を報告すると x と y の色要素の一番、環境光センサー ドライバーは、また PKEY_SensorData_LightChromaticityX、PKEY_SensorData_LightChromaticityY と PKEY_SensorData_LightTemperature_Kelvins をサポートする必要がありますしきい値。
環境光センサー ドライバーでは、読み取りセンサー クラスの拡張機能は、PKEY_SensorData_LightChromaticityX、PKEY_SensorData_LightChromaticityY または PKEY_SensorData_LightTemperature_Kelvins しきい値のいずれかが満たされたときにサンプルを報告します。

環境光センサー ドライバーは、センサー クラスの拡張機能の呼び出し直後に、1 つの例に読み取り常に報告する必要があります、 [EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)しきい値の値に関係なくコールバック。 このサンプルは、サンプルの初期読み込みと呼ばれます。

>**注**  環境光センサー ドライバーは、IsValid のデータが設定されているしきい値に関係なく、変更をフィールドとセンサー クラスの拡張機能に読み取るサンプルにも報告する必要があります。

PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference と PKEY_SensorData_LightLevel_Lux は 0.0f に設定されている、ドライバーは、間隔でサンプル測定値、センサー クラスの拡張機能を報告する必要があります。
ときに PKEY_SensorData_LightChromaticityX__または__PKEY_SensorData_LightChromaticityY__または__0.0f PKEY_SensorData_LightTemperature_Kelvins が設定されている、ドライバーは、サンプルの測定値を報告する必要があります、センサーは、すべての間隔で拡張機能をクラスします。
センサー サンプルの間隔でレポートと呼びます*センサー サンプル ストリーミング*します。

>[!NOTE]
> しきい値のモードでレポートしません鍵の連続したサンプル\_SensorData\_IsValid が FALSE に設定します。 つまり、しきい値のモードでのみ、最初のサンプルで送信する鍵\_SensorData\_IsValid を FALSE に切り替えることができます。
 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 






