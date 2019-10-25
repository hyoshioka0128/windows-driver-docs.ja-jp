---
title: 万歩計データ フィールド
description: このトピックでは、pedometer に固有のデータフィールドについて説明します。
ms.assetid: 35E52085-9727-465D-B6EF-D95974423CD5
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 77fc66643f0573c7cc3791ac0a8fb90608e9ae50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845504"
---
# <a name="pedometer-data-fields"></a>万歩計データ フィールド


このトピックでは、pedometer に固有のデータフィールドについて説明します。

次の表は、データフィールドを示しています。 **[型]** 列に表示されるデータ型の詳細については、「 [propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_PedometerStepType|VT_UI4|必須かどうか|ステップの種類。 [PEDOMETER_STEP_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type)値として表現されます。|
|PKEY_SensorData_PedometerStepCount|VT_UI4|必須かどうか|検出されたステップの数。|
|PKEY_SensorData_PedometerStepDuration_Ms|VT_I8|必須かどうか|Pedometer がステップをカウントする期間。 この値は、ミリ秒単位で表されます。|
|PKEY_SensorData_PedometerReset|VT_BOOL|必須かどうか|Pedometer がリセットされたことを示します。|

 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

[**PEDOMETER\_STEP\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-pedometer_step_type)

 

 






