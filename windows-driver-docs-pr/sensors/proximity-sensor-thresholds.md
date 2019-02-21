---
title: 近接センサーのしきい値
description: このトピックでは、センサーのしきい値が近接検索に関する情報を提供します。
ms.assetid: AD93421B-4787-4E56-B01D-58027EFEAC2D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c74b23e558e490338b82963f6b06abc7e5e29b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557846"
---
# <a name="proximity-sensor-thresholds"></a>近接センサーのしきい値

近接センサーに対して定義されている構成可能なしきい値はありません。

近接センサー ドライバーは、読み取りは呼び出すことによって、センサー クラスの拡張機能サンプルを報告する必要があります[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/nf-sensorscx-sensorscxsensordataready) PKEY_SensorData_ProximityDetection 値が変更されるたびにします。
PKEY_SensorData_ProximityDetection が変わっていなければ、近接センサー ドライバーはクラスの拡張機能に行 2 つの近接測定値で報告されませんする必要があります。

ただし、近接センサー ドライバーは、センサー クラスの拡張機能の呼び出し直後に、1 つの例に読み取り常に報告する必要があります、 [EvtSensorStart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorscx/ns-sensorscx-_sensor_controller_config)コールバック。 このサンプルと呼ばれると呼ばれる*サンプル読み取りの初期*します。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)



