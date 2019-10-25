---
title: KSK プロパティ\_ストリーム\_MASTERCLOCK
description: KSK プロパティ\_STREAM\_MASTERCLOCK プロパティは省略可能なプロパティであり、pin が同期に使用できるマスタークロックを使用または生成する場合に実装する必要があります。
ms.assetid: b8fb4d7b-e2e3-498c-9f76-4075d3ae0cb2
keywords:
- KSPROPERTY_STREAM_MASTERCLOCK ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_MASTERCLOCK
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49b2baac5c511e5a71a4024f3af80e1bab767b97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844953"
---
# <a name="ksproperty_stream_masterclock"></a>KSK プロパティ\_ストリーム\_MASTERCLOCK


KSK プロパティ\_STREAM\_MASTERCLOCK プロパティは省略可能なプロパティであり、pin が同期に使用できるマスタークロックを使用または生成する場合に実装する必要があります。

## <span id="ddk_ksproperty_stream_masterclock_ks"></span><span id="DDK_KSPROPERTY_STREAM_MASTERCLOCK_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>扱え</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティは、クエリを行うときに**NULL**ハンドルを返します。 サポートは、呼び出しが正常に返されたかどうかによって決まります。

KSK プロパティ\_STREAM\_MASTERCLOCK を使用して、マスタークロックが pin によってサポートされているかどうか、またはピンの現在のマスタークロックを設定するかどうかを照会できます。 通常、これは、DirectShow のなどのグラフマネージャーを使用して行います。 マスタークロックハンドルは取得され、別の pin のマスタークロックを設定するために使用できます。また、DirectShow グラフなどのマスタークロックのユーザーモードプロキシとして使用することもできます。

Pin に時計が設定されている場合、pin は基になるファイルオブジェクトを参照し、後でそのファイルオブジェクトに対してクエリを実行できます。 ファイルハンドル自体は、ハンドルを照会したクライアントによって閉じられる必要があります。

フィルターでは、マスタークロックが生成されない場合や、他のストリームと同期する必要のないグラフの途中にあるコンバーターフィルターなど、プロパティをサポートする必要はありません。 また、プロパティを読み取り専用として使用することもできます。フィルターがマスタークロックを生成しても、外部のマスタークロックには同期しません。

「 [KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)」と「 [avstream クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-clocks)」も参照してください。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






