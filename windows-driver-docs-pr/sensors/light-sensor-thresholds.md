---
title: 光センサーのしきい値
description: このトピックでは、光センサーのしきい値について説明します。
ms.assetid: A120601A-A5CE-4778-94A9-97E71B721E9B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f686d291f890c912d3929799db9fb2b9687657b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842454"
---
# <a name="light-sensor-thresholds"></a>光センサーのしきい値


このトピックでは、光センサーのしきい値について説明します。

次の表は、ドライバーのライトセンサーの既定のしきい値を示しています。 光センサーの既定の間隔は 10 Hz です。 [型] 列に表示される型の詳細については、「 [Propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|種類|必須/オプション|既定値|説明|
|---|---|---|---|---|
|PKEY_SensorData_LightLevel_Lux|VT_R4|必須|0.25 f|しきい値に達するために必要な照度の最小変更量。 lux の割合で計測されます。 値 0.25 f は、照度で25% の変化を意味します。|
|PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference|VT_R4|省略可能|1.0f|Lux で測定されたしきい値に達するために必要な照度の最小変更量。 値 1.0 f は、照度での1つの lux の変更を意味します。 <br>__注:__ ポータブルデバイスでは、このしきい値を実装することを強くお勧めします。これは、低アンビエント環境でのバッテリ電力の消費を減らすのに役立ちます。|
|PKEY_SensorData_LightChromaticityX|VT_R4|色がサポートされている場合は必須です。 それ以外の場合は省略可能|0.01 f|しきい値に達するために必要な CIE 1931 x カラー座標の最小変更量。絶対差として表現されます。|
|PKEY_SensorData_LightChromaticityY|VT_R4|色がサポートされている場合は必須です。 それ以外の場合は省略可能|0.01 f|しきい値に達するために必要な CIE 1931 y カラー座標の最小変更量。絶対差として表現されます。|
|PKEY_SensorData_LightTemperature_Kelvins|VT_R4|色がサポートされている場合は必須です。 それ以外の場合は省略可能|50.0 f|しきい値に達するために必要な光温度の最小変更量 (Kelvins で測定)。|

ライトセンサーは、 *LUX 値が変更された場合にのみ*、新しいデータサンプルを報告する必要があります。 この推奨レポートモデルでは、完全に暗いゼロ (0) の LUX 環境にあるときに、ライトセンサーが新しいデータサンプルを繰り返し報告しないようにします。

PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が指定されていない場合、PKEY_SensorData_LightLevel_Lux しきい値に達したときに[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)を呼び出すことによって、アンビエント光センサードライバーはセンサークラス拡張に対するサンプル読み取りを報告する必要があります。 PKEY_SensorData_LightLevel_Lux しきい値は、lux の違いに対する割合として表されます。 たとえば、このしきい値を 0.25 f に設定し、センサークラスの拡張機能に報告された最後のサンプルが 40 lux の場合、報告される次のサンプルは 30 lux より小さいか、50 lux (+/-25% of 40) よりも大きい値である必要があります。
PKEY_SensorData_LightLevel_Lux に加えて PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が指定されている場合、__両方__のしきい値が満たされている場合、アンビエント光センサーはセンサークラスの拡張機能のサンプル読み取りを報告する必要があります。 たとえば、PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が 4.0 Lux に設定され、PKEY_SensorData_LightLevel_Lux が 0.25 (つまり25%) に設定されているとします。センサークラス拡張に報告された最後のサンプル読み取りの値が 4 lux の場合、最も制限の厳しいしきい値は PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference です。 したがって、次に報告されるサンプルの読み取りは、0 lux または 8 lux である必要があります。
PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が 4.0 Lux に設定され、PKEY_SensorData_LightLevel_Lux が0.25 に設定されている場合 (つまり、25%)しかし、センサークラス拡張に報告された最後のサンプル読み取りの値は 40 lux であり、最も制限の厳しいしきい値は PKEY_SensorData_LightLevel_Lux です。 この場合、次に報告されるサンプルの読み取りは、30 lux または 50 lux である必要があります。
PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference が PKEY_SensorData_LightLevel_Lux なしで設定されることはありません。

センサードライバーが x と y の色の成分を報告する場合、アンビエント光センサードライバーも PKEY_SensorData_LightChromaticityX、PKEY_SensorData_LightChromaticityY、および PKEY_SensorData_LightTemperature_Kelvins をサポートしている必要があります。しきい.
アンビエント光センサードライバーは、PKEY_SensorData_LightChromaticityX、PKEY_SensorData_LightChromaticityY、または PKEY_SensorData_LightTemperature_Kelvins しきい値が満たされたときに、センサークラス拡張に対する読み取りのサンプルを報告します。

アンビエント光センサードライバーは、センサークラス拡張がしきい値に関係なく[Evtsensorstart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)コールバックを呼び出すと、常に1つのサンプル読み取りを報告する必要があります。 このサンプルは、最初のサンプルの読み取りとして知られています。

>また、設定されているしきい値に関係なく、IsValid データフィールドが変更された場合は、アンビエント光センサードライバーがセンサークラスの拡張機能に対する読み取りサンプルを報告する必要が**あり   ます**。

PKEY_SensorData_LightLevel_Lux_Threshold_AbsoluteDifference と PKEY_SensorData_LightLevel_Lux が 0.0 f に設定されている場合、ドライバーは、すべての間隔でセンサークラス拡張にサンプルの読み取りを報告する必要があります。
PKEY_SensorData_LightChromaticityX__また__は PKEY_SensorData_LightChromaticityY__また__は PKEY_SensorData_LightTemperature_Kelvins が 0.0 f に設定されている場合、ドライバーは、すべての間隔でセンサークラス拡張にサンプルの読み取りを報告する必要があります。
センサーサンプルをすべての間隔でレポートすることを、*センサーサンプルストリーミング*と呼びます。

>[!NOTE]
> [しきい値] モードでは、PKEY\_SensorData\_IsValid を FALSE に設定した連続したサンプルを報告しないでください。 つまり、[しきい値] モードでは、PKEY\_SensorData\_IsValid が FALSE に切り替えられた最初のサンプルのみを送信します。
 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 






