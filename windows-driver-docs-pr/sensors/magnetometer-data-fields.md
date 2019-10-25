---
title: 磁力計データ フィールド
description: このトピックでは、磁力計に固有のデータフィールドについて説明します。
ms.assetid: 5DA5566A-FECA-47ED-8338-686A548687CC
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9441bfd565bbbcce208d5b5f920e38cdb1c72248
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842452"
---
# <a name="magnetometer-data-fields"></a>磁力計データ フィールド


このトピックでは、磁力計に固有のデータフィールドについて説明します。

次の表は、データフィールドを示しています。 [型] 列に表示される型の詳細については、「 [MSDN PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_MagneticFieldStrengthX_Microteslas|VT_R4|必須かどうか|マイクロ tesラスベガスの x 軸の磁気フィールド。 これは、デバイスシャーシの磁気効果を考慮して調整されます。|
|PKEY_SensorData_MagneticFieldStrengthY_Microteslas|VT_R4|必須かどうか|マイクロ tesラスベガスの y 軸の磁気フィールド。 これは、デバイスシャーシの磁気効果を考慮して調整されます。|
|PKEY_SensorData_MagneticFieldStrengthZ_Microteslas|VT_R4|必須かどうか|Microteslas の z 軸の磁気フィールド。 これは、デバイスシャーシの磁気効果を考慮して調整されます。|
|PKEY_SensorData_MagnetometerAccuracy|VT_UI4|必須かどうか|磁力計センサーの精度。 有効な値の詳細については、「 [<strong>MAGNETOMETER_ACCURACY</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-magnetometer_accuracy)」を参照してください。|

 

## <a name="related-topics"></a>関連トピック


[**磁力計\_の精度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-magnetometer_accuracy)

[MSDN PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






