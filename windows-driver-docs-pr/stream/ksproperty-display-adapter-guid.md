---
title: KSPROPERTY\_表示\_アダプター\_GUID
description: KSPROPERTY\_表示\_アダプター\_GUID プロパティには、キャプチャ ミニドライバーのアダプターの GUID が返されます。VRAM トランスポートを使用するには、キャプチャ ミニドライバーは、このプロパティをサポートする必要があります。
ms.assetid: 419aa86e-f1c2-4fca-a9e4-87dcaaeaa2bb
keywords:
- KSPROPERTY_DISPLAY_ADAPTER_GUID ストリーミング メディア デバイス
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
ms.openlocfilehash: f18efa02f3cdbcf7bd93b4180ec7276bda6ff3ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357705"
---
# <a name="kspropertydisplayadapterguid"></a>KSPROPERTY\_表示\_アダプター\_GUID


KSPROPERTY\_表示\_アダプター\_GUID プロパティには、キャプチャ ミニドライバーのアダプターの GUID が返されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_表示\_アダプター\_GUID プロパティを取得\_を正常に完了したことを示すために成功します。 ステータスを返す場合は、プロパティ型の値が正しくない\_無効な\_パラメーター。

<a name="remarks"></a>注釈
-------

ミニドライバーは、GPU 上で、最初の先頭のアダプターの識別子を返す必要があります。

キャプチャの GUID は、キャプチャ デバイスに互換性が VRAM サブシステムを一意に識別します。 システム提供のカーネル ストリーミング (KS) プロキシ モジュール (KsProxy) では、この GUID を使用して、互換性のある VRAM サブシステム上のサーフェスを割り当てます。

この GUID、ダウン ストリームの GUID を持つレンダリングの両方をキャプチャし、ピンを表示することを確認にピン留めする AVStream 一致は、同じグラフィックス アダプターが。

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

 

 






