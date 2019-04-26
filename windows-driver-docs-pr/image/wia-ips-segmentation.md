---
title: WIA\_IP\_セグメント化
description: WIA\_IP\_セグメンテーション プロパティは、セグメント化が、スキャン中に実行するにはかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 4e801aa4-a85f-4439-8a8d-990e6cbf81e4
keywords:
- WIA_IPS_SEGMENTATION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SEGMENTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6ed0ba88a16d034ad9c9398899f766e8aa9da9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343846"
---
# <a name="wiaipssegmentation"></a>WIA\_IP\_セグメント化


WIA\_IP\_セグメンテーション プロパティは、セグメント化が、スキャン中に実行するにはかどうかを示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値:WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表は、WIA に対して定義されている値\_IP\_セグメンテーション プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_USE_SEGMENTATION_FILTER</p></td>
<td><p>アプリケーションでは、複数リージョンのスキャンのセグメント化フィルターを使用する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DONT_USE_SEGMENTATION_FILTER</p></td>
<td><p>ドライバーを作成します、子項目自体マルチリー ジョンのスキャンします。 このような状況は、スキャナーは、複数リージョンのスキャンの固定フレームを使用している場合に通常発生します。</p></td>
</tr>
</tbody>
</table>

 

WIA を実装する必要があります\_IP\_スキャナーのフラット ベッドと映画のセグメント化項目をセグメント化フィルターを使用して子項目の作成をサポートするか、ドライバー自体は固定フレームの項目の子を作成します。

セグメント化フィルターを使用してドライバーをパッケージ化し、WIA がまだあることができます\_IP\_WIA をセットのセグメント化\_不要\_使用\_セグメンテーション\_その項目の 1 つのフィルター (など、フィルムの項目の場合)。 この状況は、スキャナー、ベッドからスキャンではなく、フィルムをスキャンするために固定のフレームを使用している場合に発生する可能性があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





