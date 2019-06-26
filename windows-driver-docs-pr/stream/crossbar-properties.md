---
title: クロスバーのプロパティ
description: クロスバーのプロパティ
ms.assetid: 41e46d45-90f8-4b0c-ab27-1fec4202b711
keywords:
- クロスバー プロパティ WDK ビデオのキャプチャします。
- PROPSETID_VIDCAP_CROSSBAR
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f62edd5409102f09098662342eef3c3c99326390
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378372"
---
# <a name="crossbar-properties"></a>クロスバーのプロパティ


[PROPSETID\_しました\_クロスバー](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-crossbar)出力ピンを (対応するオーディオ、存在する場合) ビデオ入力ピンからデータのルーティングに関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_しました\_クロスバー プロパティ セット。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-can-route" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAN_ROUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-can-route)"><strong>KSPROPERTY_CROSSBAR_CAN_ROUTE</strong></a></p></td>
<td><p>特定のルーティングが可能かどうかの情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-caps)"><strong>KSPROPERTY_CROSSBAR_CAPS</strong></a></p></td>
<td><p>入力ピンの数と出力ピンの数など、クロスバーの機能を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-pininfo)"><strong>KSPROPERTY_CROSSBAR_PININFO</strong></a></p></td>
<td><p>など、データ フローの方向は、中規模の Guid をピン留めし、型をピン留め、暗証番号 (pin) の情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-route" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_ROUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-crossbar-route)"><strong>KSPROPERTY_CROSSBAR_ROUTE</strong></a></p></td>
<td><p>特定のルーティング、どの入力ピン、出力ピンの配置にルーティングするなどを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




