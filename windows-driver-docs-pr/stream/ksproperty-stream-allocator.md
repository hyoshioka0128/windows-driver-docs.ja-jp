---
title: KSK プロパティ\_STREAM\_アロケーター
description: KSK プロパティ\_STREAM\_アロケータープロパティは省略可能なプロパティであり、pin がストリームバッファーを割り当てる場合、またはアロケーターを提供できる場合に実装する必要があります。
ms.assetid: 9a13efe6-4ad4-49bc-b9f1-10c22b47d9d0
keywords:
- KSPROPERTY_STREAM_ALLOCATOR ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_ALLOCATOR
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdb64a6fbb1850fe785dcb3b99d69f6c7748ae4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844965"
---
# <a name="ksproperty_stream_allocator"></a>KSK プロパティ\_STREAM\_アロケーター


KSK プロパティ\_STREAM\_アロケータープロパティは省略可能なプロパティであり、pin がストリームバッファーを割り当てる場合、またはアロケーターを提供できる場合に実装する必要があります。

## <span id="ddk_ksproperty_stream_allocator_ks"></span><span id="DDK_KSPROPERTY_STREAM_ALLOCATOR_KS"></span>


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

戻り値は常に**NULL**ハンドルです。 ただし、呼び出しが正常に返されたかどうかによってサポートが決定されます。

プロパティは、ストリーム接続ポイントに割り当てられたアロケーターのハンドルを設定します。 KSPIN\_通信\_ソースの接続ポイントは、プロパティをチェックして、データの割り当てに使用するアロケーターのハンドルを決定します。 このプロパティは、通常、DirectShow などのグラフマネージャーによって設定されます。

アロケーターハンドルが取得され、別のフィルターピンのアロケーターを設定するために使用できます。 アロケーターを使用するフィルターでは、オブジェクトを参照して、ファイルオブジェクトへのポインターを取得し、新しいアロケーターが割り当てられたとき、または接続が閉じられたときに、ファイルオブジェクトを逆参照する必要があります。 プロパティを照会して、このコネクションポイントがアロケーターの提供をサポートしているかどうかを判断することもできます。

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

 

 






