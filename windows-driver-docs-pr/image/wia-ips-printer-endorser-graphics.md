---
title: WIA\_IP\_プリンター\_裏書き\_グラフィック
description: WIA\_IP\_プリンター\_裏書き\_・ インプリント ・/裏書き項目がテキストとグラフィックスおよびイメージ データをサポートしているかどうかを報告するグラフィックス プロパティを使用します。
ms.assetid: F2550D8F-DF66-4184-909B-F0CCB68AD7C6
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e8d6874b1f1e02db8747bec06709965f8e3c85
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351154"
---
# <a name="wiaipsprinterendorsergraphics"></a>WIA\_IP\_プリンター\_裏書き\_グラフィック


**WIA\_IP\_プリンター\_裏書き\_グラフィックス**・ インプリント ・/裏書き項目がテキストとグラフィックスおよびイメージ データをサポートしているかどうかを報告するプロパティを使用します。 グラフィックスは、印刷/推奨、テキストの近くか、または背景画像として、デバイスで通常使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4 (ブール値)

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

場合**WIA\_IP\_プリンター\_裏書き\_グラフィックス**サポートし、設定が 0 以外の値 (True) の値には、・ インプリント ・/機能は、グラフィック データをサポートしています。

このプロパティは必須のすべての・ インプリント ・/裏書き項目が常に 0 (False) の値をレポートに実装できます。

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

 

 





