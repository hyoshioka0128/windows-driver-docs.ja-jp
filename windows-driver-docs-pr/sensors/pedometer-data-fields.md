---
title: データ フィールドの歩数計
description: このトピックでは、歩数計に固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f270cda0552421c0d71efedf490e8c833c7ce12e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557848"
---
# <a name="pedometer-data-fields"></a>データ フィールドの歩数計


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

 

 






