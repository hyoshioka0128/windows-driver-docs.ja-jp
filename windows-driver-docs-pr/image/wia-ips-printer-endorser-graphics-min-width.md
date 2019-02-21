---
title: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_幅
description: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_WIA と共に幅プロパティ\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_幅、WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_高さ、および WIA\_のipアドレス\_プリンター\_裏書き\_グラフィックス\_最大\_高さが最小値と最大のサイズをレンダリングする・ インプリント ・/機能をアップロードするイメージのピクセル単位での報告に使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: D79D21FA-494F-4EB2-A3C3-7804765998E4
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MIN_WIDTH イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MIN_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 44168a96dd45726bee028b6c8b4f2c5d4191b46d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558936"
---
# <a name="wiaipsprinterendorsergraphicsminwidth"></a>WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_幅


**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_幅**プロパティと共に[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_幅**](wia-ips-printer-endorser-graphics-max-width.md)、 [ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_高さ**](wia-ips-printer-endorser-graphics-min-height.md)、および[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_高さ**](wia-ips-printer-endorser-graphics-max-height.md) ・ インプリント ・をアップロードするイメージのピクセル単位で、最小値と最大サイズを報告するために使用/裏書きを表示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

報告される値はの**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_幅**について報告された値未満でなければなりません[**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_幅**](wia-ips-printer-endorser-graphics-max-width.md)します。 報告される値はの[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_高さ**](wia-ips-printer-endorser-graphics-min-height.md)未満である必要があります値に等しいまたはそれよりも報告[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_高さ**](wia-ips-printer-endorser-graphics-max-height.md). WIA ミニドライバーは、任意のサイズのイメージを受け入れることを示すためにこれらすべてのプロパティの値が 0 を報告できます。

0 以外の値が報告された場合、WIA アプリケーション クライアントはしないでくださいとが、最小値よりも小さいか、これらのプロパティを通じて WIA ミニドライバーによって報告された最大サイズより大きいイメージのアップロードの成功を期待しない必要があります。 WIA ミニドライバーは、イメージのサイズがサポートされている範囲と一致しない場合、イメージのアップロード要求を失敗する必要があります。

このプロパティは、必要なの 0 以外の値 (True) を報告するすべての・ インプリント ・/裏書き項目に対して有効な[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス**](wia-ips-printer-endorser-graphics.md). これらのプロパティはそれ以外の場合有効ではありません。

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

 

 





