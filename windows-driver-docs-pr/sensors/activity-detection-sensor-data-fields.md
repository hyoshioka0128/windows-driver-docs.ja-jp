---
title: アクティビティ検出センサー データのフィールド
description: このトピックでは、アクティビティ検出センサーに固有のデータフィールドについて説明します。
ms.assetid: D123C082-9E20-44C2-A9F2-DAC0E09F61B7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0359486281af6b79d9f16975241f4c20ac1d6f15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824281"
---
# <a name="activity-detection-sensor-data-fields"></a>アクティビティ検出センサー データのフィールド


このトピックでは、アクティビティ検出センサーに固有のデータフィールドについて説明します。

次の表は、データフィールドを示しています。 **[型]** 列に表示されるデータ型の詳細については、「 [propvariant 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)」を参照してください。

|プロパティキー|タスクバーの検索ボックスに|必須/オプション|説明|
| --- | --- | --- | --- |
|PKEY_SensorData_CurrentActivityState|VT_UI4|必須かどうか|[<strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)型の値として表される、現在のアクティビティの状態を示す値。|
|PKEY_SensorData_CurrentActivityStateConfidence_Percentage|VT_UI2|必須かどうか|現在のアクティビティの状態を示すのセンサーの信頼レベル。|
|PKEY_SensorData_SubscribedActivityStates|VT_UI4|必須かどうか|[<strong>ACTIVITY_STATE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)型の値として表現される、サブスクライブされたアクティビティの状態を示す値です。|
|PKEY_SensorData_ActivityStream|VT_BOOL|必須かどうか|アクティビティストリームが使用可能な場合に TRUE に設定されるブール値。|
|PKEY_SensorData_ConfidenceThreshold_Percentage|VT_UI2|必須かどうか|センサーの信頼レベルのしきい値。|
 

## <a name="related-topics"></a>関連トピック


[**アクティビティ\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-activity_state)

[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






