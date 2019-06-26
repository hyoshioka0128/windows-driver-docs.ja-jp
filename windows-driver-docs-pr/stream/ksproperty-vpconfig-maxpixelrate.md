---
title: KSPROPERTY\_VPCONFIG\_MAXPIXELRATE
description: KSPROPERTY\_VPCONFIG\_MAXPIXELRATE プロパティがピクセル形式に基づいた最大ピクセルの割合を指定し、接続のディメンション (幅 × 高さ) を指定します。
ms.assetid: 5a1e70b6-32ab-4a6c-82f7-3e6e828262a4
keywords:
- KSPROPERTY_VPCONFIG_MAXPIXELRATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_MAXPIXELRATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3711df6a20a0e794d0f83eadb86f1837c3cd3c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384286"
---
# <a name="kspropertyvpconfigmaxpixelrate"></a>KSPROPERTY\_VPCONFIG\_MAXPIXELRATE


KSPROPERTY\_VPCONFIG\_MAXPIXELRATE プロパティがピクセル形式に基づいた最大ピクセルの割合を指定し、接続のディメンション (幅 × 高さ) を指定します。

## <span id="ddk_ksproperty_vpconfig_maxpixelrate_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_MAXPIXELRATE_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksvpmaxpixelrate" data-raw-source="[&lt;strong&gt;KSVPMAXPIXELRATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksvpmaxpixelrate)"><strong>KSVPMAXPIXELRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、幅、高さ、および最大値を表す KSVPMAXPIXELRATE 構造体のビデオ ポートをサポートする 1 秒あたりのピクセルの数。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSVPMAXPIXELRATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksvpmaxpixelrate)

 

 






