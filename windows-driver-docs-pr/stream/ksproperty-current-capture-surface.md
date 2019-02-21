---
title: KSPROPERTY\_現在\_キャプチャ\_画面
description: KSPROPERTY\_現在\_キャプチャ\_サーフェスのプロパティを取得または指定した暗証番号 (pin) によって使用されるキャプチャ メモリの種類を設定します。VRAM トランスポートを使用するには、キャプチャ ミニドライバーは、このプロパティをサポートする必要があります。
ms.assetid: fcb07f74-d43a-4850-b8be-c349c92f9f9f
keywords:
- KSPROPERTY_CURRENT_CAPTURE_SURFACE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CURRENT_CAPTURE_SURFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8813c23df76d2f92ef2b8027b8f9e0afbfd0ab86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529992"
---
# <a name="kspropertycurrentcapturesurface"></a>KSPROPERTY\_現在\_キャプチャ\_画面


KSPROPERTY\_現在\_キャプチャ\_サーフェスのプロパティを取得または指定した暗証番号 (pin) によって使用されるキャプチャ メモリの種類を設定します。

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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557647" data-raw-source="[&lt;strong&gt;CAPTURE_MEMORY_ALLOCATION_FLAGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557647)"><strong>CAPTURE_MEMORY_ALLOCATION_FLAGS</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_現在\_キャプチャ\_サーフェスのステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー コードを返します。

<a name="remarks"></a>注釈
-------

無効な値は 0 です[**キャプチャ\_メモリ\_割り当て\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff557647)します。

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


[**キャプチャ\_メモリ\_割り当て\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff557647)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






