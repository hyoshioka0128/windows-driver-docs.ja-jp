---
title: 一般的なカメラ、およびスキャナーのプロパティ
description: 一般的なカメラ、およびスキャナーのプロパティ
ms.assetid: 7d988a1b-4c2f-43f7-be09-a250d9ede35c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4325b3ea9918e5e03669860fde32add1da1bc879
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560407"
---
# <a name="common-camera-and-scanner-properties"></a>一般的なカメラ、およびスキャナーのプロパティ





WIA プロパティは、デバイス (ルート) または項目 (子) のいずれかの属性です。 デバイスのプロパティには、製造元の名前、その型 (スキャナーまたはカメラ) と、デバイスの説明など、デバイスに関する情報が含まれます。 項目プロパティには、項目の名前はキャプチャされた場合など、特定の項目についての情報が含まれます。 デバイスのプロパティは、WIA で識別される\_アイテムのプロパティは、名前付け規則; D、WIA で識別\_名前付け規則は。

WIA プロパティ名の途中で 3 文字の頭字語には、プロパティの型に関する情報が含まれています: は汎用的なデバイス情報のプロパティ (DIP)、デバイスのプロパティ (DPA、DPC、または DP)、またはアイテムのプロパティ (IPA、IPC、または ip アドレス)。 デバイスおよび項目のプロパティは、デバイス (DPA と IPA) の両方の種類に共通する、カメラ (DPC または IPC) に固有またはスキャナー (DP と IP) を特定することができます。 次の表は、WIA プロパティ型の一覧し、各型の例を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティの型</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DIP_<em>Xxx</em></p></td>
<td><p>デバイス情報のプロパティ</p>
<p>セットアップとインストール情報スキャナーとカメラの両方のデバイスに共通です。 WIA サービスは、これらのプロパティを提供します。 ミニドライバーは提供されません。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPA_<em>Xxx</em></p></td>
<td><p>デバイスのプロパティすべて</p>
<p>接続の状態とデバイスの時刻など、スキャナーとカメラの両方のデバイスに共通する情報。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_<em>Xxx</em></p></td>
<td><p>Item プロパティをすべて</p>
<p>項目など、スキャナーとカメラの両方のアイテムに共通する情報&#39;の名前と画像の種類。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPC_<em>Xxx</em></p></td>
<td><p>デバイス プロパティ、カメラ</p>
<p>撮った写真の数など、カメラのデバイスに固有の情報です。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPC_<em>Xxx</em></p></td>
<td><p>項目のプロパティ、カメラ</p>
<p>サムネイル画像の幅と高さなどのカメラのアイテムに固有の情報です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_<em>Xxx</em></p></td>
<td><p>デバイス プロパティ、スキャナー</p>
<p>ベッドのサイズなど、スキャナーのデバイスに固有の情報です。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_<em>Xxx</em></p></td>
<td><p>項目のプロパティ、スキャナー</p>
<p>水平および垂直方向の解像度など、スキャナーの項目に固有である情報です。</p></td>
</tr>
</tbody>
</table>

 

参照してください[WIA プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff552739)WIA の一般的なカメラに固有とスキャナーに固有のプロパティの完全な一覧についてはします。

 

 




