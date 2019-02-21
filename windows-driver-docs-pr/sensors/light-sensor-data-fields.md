---
title: 光センサーのデータ フィールド
description: このトピックでは、光センサーに固有のデータ フィールドの詳細についての情報を提供します。
ms.assetid: 96572A6A-CACC-4B79-B63C-5554C07F7C83
ms.date: 01/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f731ab9f09c2776063f610fbc653d7ae78d7f60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557343"
---
# <a name="light-sensor-data-fields"></a>光センサーのデータ フィールド


このトピックでは、光センサーに固有のデータ フィールドの詳細についての情報を提供します。

次の表では、データ フィールドを示します。 型の列に示すように種類の詳細については、次を参照してください。 [PROPVARIANT 構造](https://go.microsoft.com/fwlink/p/?linkid=313395)します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティのキー</th>
<th>種類</th>
<th>必須/オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorData_LightLevel_Lux</p></td>
<td><p>VT_R4</p></td>
<td><p>必須</p></td>
<td><p>Lux ルクスのレベル。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_LightTemperature_Kelvins</p></td>
<td><p>VT_R4</p></td>
<td><p>省略可能</p></td>
<td><p>ケルビンでライト温度。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_LightChromaticityX</p></td>
<td><p>VT_R4</p></td>
<td><p>省略可能</p></td>
<td><p>CIE 1931 が一番のダイアグラムに x の色を調整します。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_LightChromaticityY</p></td>
<td><p>VT_R4</p></td>
<td><p>省略可能</p></td>
<td><p>CIE 1931 が一番の図は、y の色を調整します。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_IsValid</p></td>
<td><p>VT_BOOL</p></td>
<td><p>省略可能</p></td>
<td><p>環境光センサーは、任意の有効なサンプルを返すことができない現在ときに、この値を FALSE に設定する必要があります。 たとえば、ビューのセンサー フィールドは、(オブジェクト、またはユーザーの手をする場合など、センサーの前に) 障害物がある場合は、この値を FALSE に設定可能性があります。 環境光センサーのアンビエント ライトを正確に判断できる場合、この値を TRUE に設定する必要があります。 時間を最小限に抑える適切なハードウェアの設計する必要があり、ようを FALSE に設定するには、この値を必要とするシナリオのシナリオで、明るさを適切に制御すると、システムができなくなります。 理想的なシステムで、この値は常に TRUE に設定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






