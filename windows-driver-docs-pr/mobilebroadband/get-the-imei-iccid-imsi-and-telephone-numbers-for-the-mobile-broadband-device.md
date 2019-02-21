---
title: MB デバイスの IMEI、ICCID、IMSI、および電話番号を取得します。
description: モバイル ブロード バンド デバイスの IMEI、ICCID、IMSI および電話番号を取得します。
ms.assetid: b604d08c-7e6f-4dad-9e1d-3f24a0da5760
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fc18008347d3c4257079311954f62724860f20c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532495"
---
# <a name="get-the-imei-iccid-imsi-and-telephone-numbers-for-the-mobile-broadband-device"></a>モバイル ブロード バンド デバイスの IMEI、ICCID、IMSI および電話番号を取得します。


アカウントの現在のネットワーク デバイスの使用可能なは、次のプロパティです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>使用する MobileBroadbandDeviceInformation のプロパティ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IMEI</p></td>
<td><p>MobileEquipmentId</p></td>
</tr>
<tr class="even">
<td><p>MEID</p></td>
<td><p>MobileEquipmentId</p></td>
</tr>
<tr class="odd">
<td><p>IMSI</p></td>
<td><p>サブスクライバー Id</p></td>
</tr>
<tr class="even">
<td><p>最小値</p></td>
<td><p>サブスクライバー Id</p></td>
</tr>
<tr class="odd">
<td><p>IRM</p></td>
<td><p>サブスクライバー Id</p></td>
</tr>
<tr class="even">
<td><p>ICCID</p></td>
<td><p>SimIccId</p></td>
</tr>
<tr class="odd">
<td><p>電話番号</p></td>
<td><p>TelephoneNumbers (ネットワークの登録後にのみ使用可能)</p></td>
</tr>
</tbody>
</table>

 

``` syntax
account.currentDeviceInformation.mobileEquipmentId
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






