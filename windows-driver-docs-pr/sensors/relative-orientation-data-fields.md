---
title: 相対方向センサー データ フィールド
description: このトピックでは、相対的な方向センサーに固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: A48B75DD-5424-48CC-AC8B-251874414FCE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 435b906ec74bd1c76d6365324f5de40af44d6a16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358540"
---
# <a name="relative-orientation-sensor-data-fields"></a>相対方向センサー データ フィールド


このトピックでは、相対的な方向センサーに固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、次を参照してください。 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_Timestamp|VT_FILETIME|必須|サンプリングされたデータのタイムスタンプ。 各サンプルは、センサー ドライバーによって報告されるために必要です。|
|PKEY_SensorData_QuaternionW|VT_R4|必須|(複素数の虚数部の部分) ではなく実際の係数。|
|PKEY_SensorData_QuaternionX|VT_R4|必須|回転の軸のベクターの X 成分。|
|PKEY_SensorData_QuaternionY|VT_R4|必須|回転の軸のベクターの X 成分。|
|PKEY_SensorData_QuaternionZ|VT_R4|必須|回転の軸のベクターの X 成分。|

 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






