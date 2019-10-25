---
title: 近接センサーのしきい値
description: このトピックでは、近接センサーのしきい値について説明します。
ms.assetid: AD93421B-4787-4E56-B01D-58027EFEAC2D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8efc03ba23371194e488235e2d5e74f08b0f81dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841762"
---
# <a name="proximity-sensor-thresholds"></a>近接センサーのしきい値

近接センサーには、構成可能なしきい値が定義されていません。

近接センサードライバーは、PKEY_SensorData_ProximityDetection 値が変更されるたびに[SensorsCxSensorDataReady](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/nf-sensorscx-sensorscxsensordataready)を呼び出すことによって、センサークラス拡張に対するサンプル読み取りを報告する必要があります。
近接センサードライバーは、PKEY_SensorData_ProximityDetection が変更されていない限り、クラスの拡張に対して2つの近接した読み取りを報告しないようにする必要があります。

ただし、センサークラスの拡張機能によって[Evtsensorstart](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorscx/ns-sensorscx-_sensor_controller_config)コールバックが呼び出された直後に、近接センサードライバーが1つのサンプル読み取りを常に報告する必要があります。 このサンプルは、「*最初のサンプルの読み取り*」と呼ばれています。

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)



