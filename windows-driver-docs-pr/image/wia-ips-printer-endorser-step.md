---
title: WIA\_IP\_プリンター\_裏書き\_手順
description: 既定では、・ インプリント ・/機能についているまたは、各ドキュメントのページがスキャンするには。
ms.assetid: A4455204-6502-4BE7-9EE3-B5616089FA05
keywords:
- WIA_IPS_PRINTER_ENDORSER_STEP イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_STEP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a0b583f55276e4dd246f66a7c9a8d74e7a8a943
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351182"
---
# <a name="wiaipsprinterendorserstep"></a>WIA\_IP\_プリンター\_裏書き\_手順


既定では、・ インプリント ・/機能についているまたは、各ドキュメントのページがスキャンするには。 使用して、クライアントによってこの必須の既定の動作を変更できる、 **WIA\_IP\_プリンター\_裏書き\_手順**プロパティ。 たとえば、クライアント アプリケーションでは、2 ページがあるすべての他のスキャンした彫り動作保証済み (0、2、4、6、...) を現在の値を設定できます。WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

必須の既定値、 **WIA\_IP\_プリンター\_裏書き\_手順**プロパティが 1 (各 ページ)。 0 の値が無効です。

WIA のほとんどの場合と\_PROP\_範囲のプロパティ、WIA ミニドライバーは 1 つ 1 つの値、最大最小値と等しいおよび 0 のステップ値を含む範囲を実装できます。

このプロパティは、すべて・ インプリント ・/裏書きデータ ソース アイテムをサポートする必要があります。 1 (各 ページ) の値が必要です。

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

 

 





