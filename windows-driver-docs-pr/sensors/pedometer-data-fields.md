---
title: 万歩計データ フィールド
description: このトピックでは、歩数計に固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f270cda0552421c0d71efedf490e8c833c7ce12e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330090"
---
# <a name="pedometer-data-fields"></a>万歩計データ フィールド


このトピックでは、歩数計に固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 示されるデータ型の詳細については、**型**列を参照してください[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_PedometerStepType|VT_UI4|必須|表される、ステップの種類、 [PEDOMETER_STEP_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-pedometer_step_type)値。|
|PKEY_SensorData_PedometerStepCount|VT_UI4|必須|検出されたステップ数。|
|PKEY_SensorData_PedometerStepDuration_Ms|VT_I8|必須|歩数計が手順をカウントする期間です。 この値は、ミリ秒単位で表されます。|
|PKEY_SensorData_PedometerReset|VT_BOOL|必須|歩数計がリセットされたことを示します。|

 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**歩数計\_手順\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-pedometer_step_type)

 

 






