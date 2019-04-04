---
title: 相対的な方向センサーのデータ フィールド
description: このトピックでは、相対的な方向センサーに固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: A48B75DD-5424-48CC-AC8B-251874414FCE
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 435b906ec74bd1c76d6365324f5de40af44d6a16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557847"
---
# <a name="relative-orientation-sensor-data-fields"></a>相対的な方向センサーのデータ フィールド


このトピックでは、相対的な方向センサーに固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、[PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)を参照してください。

|プロパティのキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_Timestamp|VT_FILETIME|必須|サンプリングされたデータのタイムスタンプ。 各サンプルは、センサー ドライバーによって報告されるために必要です。|
|PKEY_SensorData_QuaternionW|VT_R4|必須|(複素数の虚数部の部分) ではなく実際の係数。|
|PKEY_SensorData_QuaternionX|VT_R4|必須|回転の軸のベクターの X 成分。|
|PKEY_SensorData_QuaternionY|VT_R4|必須|回転の軸のベクターの X 成分。|
|PKEY_SensorData_QuaternionZ|VT_R4|必須|回転の軸のベクターの X 成分。|

 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






