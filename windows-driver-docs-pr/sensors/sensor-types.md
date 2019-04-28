---
title: センサーの種類
description: ユニバーサル センサーの種類の Guid
ms.assetid: AD1112ED-4EA8-429D-82E6-D1878447D5E3
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9133ccddc7afcef70e4b80c841b5a9e65226fb88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368809"
---
# <a name="sensor-types"></a>センサーの種類

このセクションは、センサーの種類ごとに関連付けられている Guid のセンサーの種類に関する情報を提供します。 センサーの種類は、特定の種類のセンサーを表します。 各センサーの種類は、特定のカテゴリに適合できます必要に応じて。

センサーの種類の Guid は Sensorsdef.h で定義されます。

| 名前 | 説明 |
| --- | --- |
| GUID_SensorType_Accelerometer3D | この GUID は、加速度計を識別します。 |
| GUID_SensorType_ActivityDetection | この GUID は、アクティビティの検出のセンサーを識別します。 |
| GUID_SensorType_AmbientLight | この GUID は、環境光センサーを識別します。 |
| GUID_SensorType_Barometer | この GUID は、バロメーターを識別します。 |
| GUID_SensorType_Custom | この GUID は、カスタム センサーを識別します。 |
| GUID_SensorType_GeomagneticOrientation | この GUID は、geomagnetic の向きを識別します。 |
| GUID_SensorType_GravityVector | この GUID は、重力ベクトルを識別します。 |
| GUID_SensorType_Gyrometer3D | この GUID は、ジャイロ メーターを識別します。 |
| GUID_SensorType_Humidity | この GUID は、湿度センサーを識別します。 |
| GUID_SensorType_LinearAccelerometer | この GUID は、線形の加速度計を識別します。 |
| GUID_SensorType_Magnetometer3D | この GUID は、磁力計を識別します。 |
| GUID_SensorType_Orientation | この GUID は、方向センサーを識別します。 |
| GUID_SensorType_Pedometer | この GUID は、歩数計を識別します。 |
| GUID_SensorType_Proximity | この GUID は、近接センサーを識別します。 |
| GUID_SensorType_RelativeOrientation | この GUID は、RelativeOrientation センサーを識別します。 |
| GUID_SensorType_SimpleDeviceOrientation | この GUID は、単純なデバイスの方向センサーを識別します。 |
| GUID_SensorType_Temperature | この GUID は、温度センサーを識別します。 |

>[!NOTE]
> Compass と傾斜計センサーは、Windows ユニバーサル センサー DDI で直接は公開されません。 代わりに、これら 2 つのセンサーは GUID_SensorType_Orientation センサーの上にセンサー スタックによって自動的に作成されます。
> GUID_SensorType_Orientation センサーが、システム上に存在する場合に、コンパスと傾斜計を WinRT アプリケーションに表示されることがなります。 同様に、高度計センサーは GUID_SensorType_Barometer センサーの上にセンサー スタックによって自動的に構築されます。


