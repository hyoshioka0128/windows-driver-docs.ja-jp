---
title: Geomagnetic 向き
description: このトピックでは、geomagnetic 方向センサーに固有のデータ フィールドに関する情報を提供します。
ms.assetid: C164E5A9-A664-4EE5-91CE-918233DFFB6D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 619f6a6b1b6609bc36ab07508fea5c2695538910
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366693"
---
# <a name="geomagnetic-orientation"></a>地磁気の方向


このトピックでは、geomagnetic 方向センサーに固有のデータ フィールドに関する情報を提供します。

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
<th>説明/コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PKEY_SensorData_QuaternionW</p></td>
<td><p>VT_R4</p></td>
<td><p>必須</p></td>
<td><p>(複素数の虚数部の部分) ではなく実際の係数。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_QuaternionX</p></td>
<td><p>VT_R4</p></td>
<td><p>必須</p></td>
<td><p>回転の軸のベクターの X 成分。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_QuaternionY</p></td>
<td><p>VT_R4</p></td>
<td><p>必須</p></td>
<td><p>回転の軸のベクターの Y 成分。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_QuaternionZ</p></td>
<td><p>VT_R4</p></td>
<td><p>必須</p></td>
<td><p>回転の軸のベクトルの Z 成分。</p></td>
</tr>
<tr class="odd">
<td><p>PKEY_SensorData_DeclinationAngle_Degrees</p></td>
<td><p>VT_R4</p></td>
<td><p>必須</p></td>
<td><p>拒否の角度。 サポートされていない場合、クラス拡張はこの値を計算します。</p></td>
</tr>
<tr class="even">
<td><p>PKEY_SensorData_RotationAngle_Degrees</p></td>
<td><p>VT_R4</p></td>
<td><p>Windows 10 Mobile に必要な</p>
<p>Windows 10 デスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) (省略可能)</p></td>
<td><p>回転の角度 (度単位)。</p>
<p>デバイスの向きのセンサーを公開するドライバーは、しきい値キーのこのプロパティのキーを使用する必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PROPVARIANT 構造体](https://go.microsoft.com/fwlink/p/?linkid=313395)

 

 






