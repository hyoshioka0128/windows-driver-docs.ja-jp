---
title: KSPROPERTY\_ストリーム\_低下
description: KSPROPERTY\_ストリーム\_低下プロパティが省略可能なプロパティ、暗証番号 (pin) がパフォーマンス低下の戦略を許可する場合に実装する必要があります。
ms.assetid: b8f9db81-a9ed-4a13-8d64-14854193c91b
keywords:
- KSPROPERTY_STREAM_DEGRADATION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_DEGRADATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40350124803ca03d65941b025d3d994a0a8a7c25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539654"
---
# <a name="kspropertystreamdegradation"></a>KSPROPERTY\_ストリーム\_低下


KSPROPERTY\_ストリーム\_低下プロパティが省略可能なプロパティ、暗証番号 (pin) がパフォーマンス低下の戦略を許可する場合に実装する必要があります。

## <span id="ddk_ksproperty_stream_degradation_ks"></span><span id="DDK_KSPROPERTY_STREAM_DEGRADATION_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff561671" data-raw-source="[&lt;strong&gt;KSDEGRADE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561671)"> <strong>KSDEGRADE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

返される構造体の数とサイズ プロパティを返すクエリを実行時に[ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)形式、続けて[ **KSDEGRADE**](https://msdn.microsoft.com/library/windows/hardware/ff561671)構造体。

クエリでこのプロパティを返します KSMULTIPLE で返される構造体の数とサイズ\_KSDEGRADE 構造体の後に、項目の形式。 複数の項目の形式は、クエリを実行して低下戦略の設定の両方で使用する必要があります。

クライアントは、現在のパフォーマンス低下の設定を取得するには、このプロパティにクエリを実行または現在のパフォーマンス低下の設定を変更するには、このプロパティを設定できます。 品質管理 (QM) 準拠への応答フィルターのピン留めしてリソースの使用量を変更する、またはいくつかのより高いレベルに戻すの品質を調整する、パフォーマンス低下の設定が使用されます。 これは通常使用品質マネージャーによって低下の設定を調整し、調整できる設定とその現在の値の型のクエリを実行します。 値を設定するときに、複数の KSDEGRADE 構造体を渡すこと可能性があります。 品質のマネージャーの詳細については、次を参照してください。[品質管理](https://msdn.microsoft.com/library/windows/hardware/ff568124)します。

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

[**KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)

[**KSDEGRADE**](https://msdn.microsoft.com/library/windows/hardware/ff561671)

 

 






