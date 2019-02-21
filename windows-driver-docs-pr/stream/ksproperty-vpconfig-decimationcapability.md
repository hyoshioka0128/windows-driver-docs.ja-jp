---
title: KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY
description: KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY プロパティは、ハードウェアでのビデオ画像のサイズを削減できるかどうかを示します。
ms.assetid: a929b154-165e-4075-9295-d34fecc8e18d
keywords:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a5844e0d8918bc423fdad8fc248759d76fecc86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531049"
---
# <a name="kspropertyvpconfigdecimationcapability"></a>KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY


KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY プロパティは、ハードウェアでのビデオ画像のサイズを削減できるかどうかを示します。

## <span id="ddk_ksproperty_vpconfig_decimationcapability_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY_KS"></span>


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
<td><p>X</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>ブール値</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ブール値です。 指定**TRUE**かどうかハードウェアはビデオ画像のサイズを減らすか、指定**FALSE**ハードウェアは、ディメンションを減らすことができない場合。

<a name="remarks"></a>注釈
-------

プロパティの値の**TRUE**サイズの画像を小さくできることを指定します。 **FALSE**クリッピング四角形にも、イメージ サイズ変更ができる、ことを指定しますの代わりにスケールします。

KSPROPERTY\_VPCONFIG\_デシメーション\_機能プロパティの要求が状態を返す\_を正常に完了を示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

KSPROPSETID でこのプロパティを使用するときに\_VPVBIConfig、プロパティのすべての要求は状態を返す必要があります\_いない\_実装されていません。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






