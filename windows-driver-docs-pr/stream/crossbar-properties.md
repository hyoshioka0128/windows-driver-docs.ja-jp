---
title: クロスバーのプロパティ
description: クロスバーのプロパティ
ms.assetid: 41e46d45-90f8-4b0c-ab27-1fec4202b711
keywords:
- クロスバー プロパティ WDK ビデオのキャプチャします。
- PROPSETID_VIDCAP_CROSSBAR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a1cbf2e50f7127c05801abf08ed14a4d8b2bb4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374163"
---
# <a name="crossbar-properties"></a>クロスバーのプロパティ


[PROPSETID\_しました\_クロスバー](https://msdn.microsoft.com/library/windows/hardware/ff567804)出力ピンを (対応するオーディオ、存在する場合) ビデオ入力ピンからデータのルーティングに関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_しました\_クロスバー プロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_CROSSBAR KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565117" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAN_ROUTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565117)"><strong>KSPROPERTY_CROSSBAR_CAN_ROUTE</strong></a></p></td>
<td><p>特定のルーティングが可能かどうかの情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565118" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565118)"><strong>KSPROPERTY_CROSSBAR_CAPS</strong></a></p></td>
<td><p>入力ピンの数と出力ピンの数など、クロスバーの機能を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565121" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565121)"><strong>KSPROPERTY_CROSSBAR_PININFO</strong></a></p></td>
<td><p>など、データ フローの方向は、中規模の Guid をピン留めし、型をピン留め、暗証番号 (pin) の情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565126" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565126)"><strong>KSPROPERTY_CROSSBAR_ROUTE</strong></a></p></td>
<td><p>特定のルーティング、どの入力ピン、出力ピンの配置にルーティングするなどを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




