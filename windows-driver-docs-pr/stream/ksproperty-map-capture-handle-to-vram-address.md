---
title: KSK プロパティ\_\_VRAM\_アドレスに\_を処理\_ハンドル\_マップします
description: KSK プロパティ\_マップ\_CAPTURE\_ハンドル\_を\_VRAM\_ADDRESS プロパティにマップして、vram サーフェイスハンドルから VRAM 物理アドレスへのキャプチャドライバーのマッピングを返します。VRAM トランスポートを使用するには、capture ミニドライバーがこのプロパティをサポートしている必要があります。
ms.assetid: 071c9152-12f9-4ec1-80d7-6b42fce51bbb
keywords:
- KSPROPERTY_MAP_CAPTURE_HANDLE_TO_VRAM_ADDRESS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_MAP_CAPTURE_HANDLE_TO_VRAM_ADDRESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0894363f69405b0d71d2dd470e596386fcf9105
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838049"
---
# <a name="ksproperty_map_capture_handle_to_vram_address"></a>KSK プロパティ\_\_VRAM\_アドレスに\_を処理\_ハンドル\_マップします


KSK プロパティ\_マップ\_CAPTURE\_ハンドル\_を\_VRAM\_ADDRESS プロパティにマップして、vram サーフェイスハンドルから VRAM 物理アドレスへのキャプチャドライバーのマッピングを返します。

VRAM トランスポートを使用するには、capture ミニドライバーがこのプロパティをサポートしている必要があります。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s" data-raw-source="[&lt;strong&gt;VRAM_SURFACE_INFO_PROPERTY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-vram_surface_info_property_s)"><strong>VRAM_SURFACE_INFO_PROPERTY_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_マップ\_キャプチャ\_ハンドル\_を\_VRAM\_に割り当てて、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラーコードを返します。

<a name="remarks"></a>注釈
-------

キャプチャドライバーは、このプロパティのハンドラーでマッピングを実行する必要があります。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






