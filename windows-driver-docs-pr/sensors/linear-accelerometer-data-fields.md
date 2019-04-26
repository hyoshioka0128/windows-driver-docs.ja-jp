---
title: 直線加速度計データ フィールド
description: このトピックでは、線形の加速度計に固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: FD869359-C1C2-4B2F-95F3-01234331DC54
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: af80e0005d950244506d928cc8bb2a325b73a013
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345156"
---
#  <a name="linear-accelerometer-data-fields"></a>直線加速度計データ フィールド

このトピックでは、線形の加速度計に固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、次を参照してください。 [MSDN PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

|プロパティのキー|種類|必須/オプション|説明|
|--|--|--|--|
|PKEY_SensorData_AccelerationX_Gs|VT_R4|必須|G's で x 軸の高速化|
|PKEY_SensorData_AccelerationY_Gs|VT_R4|必須|G's で y 軸の高速化|
|PKEY_SensorData_AccelerationZ_Gs|VT_R4|必須|G's で z 軸の高速化|
|PKEY_SensorData_Shake|VT_BOOL|省略可能|線形の加速度計によって、シェイクが検出されたことを示します。 これはデータ フィールドは、送信される場合は true である必要があります。|

 

## <a name="related-topics"></a>関連トピック


[MSDN PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)





