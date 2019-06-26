---
title: KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス
description: KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス プロパティでは、VRAM の物理アドレスを VRAM サーフェス ハンドルのキャプチャのドライバーのマッピングを返します。VRAM トランスポートを使用するには、キャプチャ ミニドライバーは、このプロパティをサポートする必要があります。
ms.assetid: 071c9152-12f9-4ec1-80d7-6b42fce51bbb
keywords:
- KSPROPERTY_MAP_CAPTURE_HANDLE_TO_VRAM_ADDRESS ストリーミング メディア デバイス
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
ms.openlocfilehash: 39ac1ac75ff97bc37866f488b8b86e0994322768
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371145"
---
# <a name="kspropertymapcapturehandletovramaddress"></a>KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス


KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレス プロパティでは、VRAM の物理アドレスを VRAM サーフェス ハンドルのキャプチャのドライバーのマッピングを返します。

VRAM トランスポートを使用するには、キャプチャ ミニドライバーは、このプロパティをサポートする必要があります。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-vram_surface_info_property_s" data-raw-source="[&lt;strong&gt;VRAM_SURFACE_INFO_PROPERTY_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-vram_surface_info_property_s)"><strong>VRAM_SURFACE_INFO_PROPERTY_S</strong></a></p></td>
<td><p>DWORD</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_マップ\_キャプチャ\_処理\_TO\_VRAM\_アドレスは、ステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー コードを返します。

<a name="remarks"></a>注釈
-------

キャプチャ ドライバーでは、このプロパティのハンドラーでマッピングを実行する必要があります。

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

 

 






