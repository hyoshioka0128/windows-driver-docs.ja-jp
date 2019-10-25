---
title: KSK プロパティ\_\_アダプター\_GUID を表示します
description: '\_アダプター\_GUID プロパティを表示\_KSK プロパティは、キャプチャミニドライバーからアダプターの GUID を返します。VRAM トランスポートを使用するには、capture ミニドライバーがこのプロパティをサポートしている必要があります。'
ms.assetid: 419aa86e-f1c2-4fca-a9e4-87dcaaeaa2bb
keywords:
- KSPROPERTY_DISPLAY_ADAPTER_GUID ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DISPLAY_ADAPTER_GUID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d512cce20c766e7b88e1198c389a27268d3cde
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837549"
---
# <a name="ksproperty_display_adapter_guid"></a>KSK プロパティ\_\_アダプター\_GUID を表示します


\_アダプター\_GUID プロパティを表示\_KSK プロパティは、キャプチャミニドライバーからアダプターの GUID を返します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_アダプター\_GUID プロパティを表示\_KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 プロパティの型の値が正しくない場合は、STATUS\_INVALID\_PARAMETER が返されます。

<a name="remarks"></a>注釈
-------

ミニドライバーは、GPU の最初のヘッドのアダプター識別子を返す必要があります。

キャプチャ GUID は、キャプチャデバイスと互換性のある VRAM サブシステムを一意に識別します。 システム指定のカーネルストリーミング (KS) プロキシモジュール (Ksk プロキシ) は、この GUID を使用して、互換性のある VRAM サブシステムにサーフェイスを割り当てます。

AVStream は、キャプチャピンとレンダーピンの両方が同じグラフィックスアダプター上にあることを確認するために、この GUID とダウンストリームレンダリングピンの GUID を照合します。

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

 

 






