---
title: WIA\_IP\_しきい値
description: WIA\_IP\_しきい値プロパティには、デバイスの現在のハードウェアのしきい値の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 1d315168-5434-4e99-9e54-cb6e279df3e7
keywords:
- WIA_IPS_THRESHOLD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_THRESHOLD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f2575b6e5a51d65ad08d2e50e77b04d6fa7a70e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343834"
---
# <a name="wiaipsthreshold"></a>WIA\_IP\_しきい値


WIA\_IP\_しきい値プロパティには、デバイスの現在のハードウェアのしきい値の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_threshold_si"></span><span id="DDK_WIA_IPS_THRESHOLD_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

値は、WIA をマップする必要があります\_IP\_0 ~ 255 の範囲のしきい値のプロパティ。 既定値は 128 です。

アプリケーション設定 WIA\_IP\_ハードウェアしきい値の値を変更するしきい値。 この値は有効な場合にのみ、 [ **WIA\_IPA\_DATATYPE** ](wia-ipa-datatype.md)プロパティは WIA 等しく\_データ\_しきい値。 デバイスが WIA を許可していない場合\_データ\_しきい値を変更するには、128 の既定値を報告する必要があります。

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

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_データ型**](wia-ipa-datatype.md)

 

 






