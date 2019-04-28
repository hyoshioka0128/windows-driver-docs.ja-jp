---
title: アクティビティ検出センサー データのフィールド
description: このトピックでは、アクティビティの検出のセンサーに固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: D123C082-9E20-44C2-A9F2-DAC0E09F61B7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b05f8f13c86323edc699cc9a33a7ef6485ea3771
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376510"
---
# <a name="activity-detection-sensor-data-fields"></a>アクティビティ検出センサー データのフィールド


このトピックでは、アクティビティの検出のセンサーに固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 示されるデータ型の詳細については、**型**列を参照してください[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明|
| --- | --- | --- | --- |
|PKEY_SensorData_CurrentActivityState|VT_UI4|必須|型の値で表した現在のアクティビティの状態を示す値[ <strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-activity_state)します。|
|PKEY_SensorData_CurrentActivityStateConfidence_Percentage|VT_UI2|必須|現在のアクティビティの状態を示すでセンサーの信頼レベル。|
|PKEY_SensorData_SubscribedActivityStates|VT_UI4|必須|型の値として表される、定期受信済みアクティビティの状態を示す値[ <strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-activity_state)します。|
|PKEY_SensorData_ActivityStream|VT_BOOL|必須|アクティビティ ストリームが使用可能な場合は TRUE に設定するブール値。|
|PKEY_SensorData_ConfidenceThreshold_Percentage|VT_UI2|必須|センサーの信頼レベルのしきい値。|
 

## <a name="related-topics"></a>関連トピック


[**アクティビティ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-activity_state)

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






