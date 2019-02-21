---
title: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_高さ
description: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_WIA と共に高さプロパティ\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_の高さ、WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_幅、および WIA\_のipアドレス\_プリンター\_裏書き\_グラフィックス\_MIN\_幅が最小値と最大のサイズをレンダリングする・ インプリント ・/機能をアップロードするイメージのピクセル単位での報告に使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 96010EAE-835D-48F7-8EB4-27BAF05252A0
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MAX_HEIGHT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_MAX_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 820c4e42fc273a23f04894b4d0a6042cd92e7dee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556713"
---
# <a name="wiaipsprinterendorsergraphicsmaxheight"></a>WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_高さ


**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_高さ**プロパティと共に[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_高さ**](wia-ips-printer-endorser-graphics-min-height.md)、 [ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_幅**](wia-ips-printer-endorser-graphics-max-width.md)、および[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_幅**](wia-ips-printer-endorser-graphics-min-width.md) ・ インプリント ・をアップロードするイメージのピクセル単位で、最小値と最大サイズを報告するために使用/裏書きを表示します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

報告される値はの[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_高さ**](wia-ips-printer-endorser-graphics-min-height.md)未満である必要があります値に等しいまたはそれよりも報告**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_高さ**します。 報告される値はの[**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_MIN\_幅**](wia-ips-printer-endorser-graphics-min-width.md)必要がありますより小さいについて報告された値と等しいか[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス\_最大\_幅**](wia-ips-printer-endorser-graphics-max-width.md). WIA ミニドライバーは、任意のサイズのイメージを受け入れることを示すためにこれらすべてのプロパティの値が 0 を報告できます。

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

 

 





