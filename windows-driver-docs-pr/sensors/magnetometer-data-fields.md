---
title: 磁力計データ フィールド
description: このトピックでは、磁力計に固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: 5DA5566A-FECA-47ED-8338-686A548687CC
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d6022f46e2b7a9a57adbd9aff785ee61a1b0b30e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345123"
---
# <a name="magnetometer-data-fields"></a>磁力計データ フィールド


このトピックでは、磁力計に固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、次を参照してください。 [MSDN PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必須|Microteslas の x 軸の磁気フィールド。 これは、デバイスのシャーシの磁気効果のアカウントに調整します。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必須|Microteslas の y 軸の磁気フィールドです。 これは、デバイスのシャーシの磁気効果のアカウントに調整します。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必須|Microteslas の z 軸の磁気フィールドです。 これは、デバイスのシャーシの磁気効果のアカウントに調整します。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必須|磁力計センサーの精度。 有効な値の詳細については、次を参照してください。 [ <strong>MAGNETOMETER_ACCURACY</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-magnetometer_accuracy)します。|

 

## <a name="related-topics"></a>関連トピック


[**磁力計\_精度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-magnetometer_accuracy)

[MSDN PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






