---
title: KSPROPERTY\_ストリーム\_アロケーター
description: KSPROPERTY\_ストリーム\_アロケーター プロパティが省略可能なプロパティ、暗証番号 (pin) のストリーム バッファーを割り当てまたはアロケーターを提供することができる場合に実装する必要があります
ms.assetid: 9a13efe6-4ad4-49bc-b9f1-10c22b47d9d0
keywords:
- KSPROPERTY_STREAM_ALLOCATOR ストリーミング メディア デバイス
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
ms.openlocfilehash: d720349855711e149387112f4503ff8f025a1042
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392705"
---
# <a name="kspropertystreamallocator"></a>KSPROPERTY\_ストリーム\_アロケーター


KSPROPERTY\_ストリーム\_アロケーター プロパティが省略可能なプロパティ、暗証番号 (pin) のストリーム バッファーを割り当てまたはアロケーターを提供することができる場合に実装する必要があります

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
<td><p>ハンドル</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

返される値は常に、 **NULL**を処理します。 ただし、サポートは、呼び出しが正常に終了するかどうかによって決まります。

プロパティは、ストリームの接続ポイントに割り当てられたアロケーターのハンドルを設定します。 KSPIN のコネクション ポイント\_通信\_ソース データの割り当てに使用するアロケーターのハンドルを判別するプロパティを確認します。 このプロパティは通常、DirectShow などのグラフ マネージャーによって設定します。

アロケーターのハンドルは取得され、別のフィルターの pin のアロケーターを設定するために使用できます。 アロケーターを使用してフィルターには、ファイル オブジェクトへのポインターを取得し、新しいアロケーターが割り当てられている場合、または接続が閉じられたときに、ファイル オブジェクトを逆参照するオブジェクトを参照する必要があります。 コネクション ポイントが、アロケーターを提供することをサポートしているかどうか、プロパティを照会こともできます。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






