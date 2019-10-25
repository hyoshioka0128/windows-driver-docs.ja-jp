---
title: KSK プロパティ\_STREAM\_RATECAPABILITY
description: KSK プロパティ\_STREAM\_RATECAPABILITY プロパティを使用すると、グラフマネージャーは特定のストリームのフローに関係するすべてのコネクションポイント (KSK プロパティ\_PIN\_DATAROUTING) に関連するすべての接続ポイントをクエリし、の機能を取得できます。要求されたレートを公称レートに調整します。
ms.assetid: 73e3bf4e-2815-4890-ba12-77fbe7a7c589
keywords:
- KSPROPERTY_STREAM_RATECAPABILITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_RATECAPABILITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9afb3e1fe2cce5e2368a56aada07629dd9795b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837939"
---
# <a name="ksproperty_stream_ratecapability"></a>KSK プロパティ\_STREAM\_RATECAPABILITY


KSK プロパティ\_STREAM\_RATECAPABILITY プロパティを使用すると、グラフマネージャーは特定のストリームのフローに関係するすべてのコネクションポイント (KSK プロパティ\_PIN\_DATAROUTING) に関連するすべての接続ポイントをクエリし、の機能を取得できます。要求されたレートを公称レートに調整します。

## <span id="ddk_ksproperty_stream_ratecapability_ks"></span><span id="DDK_KSPROPERTY_STREAM_RATECAPABILITY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)"><strong>KSRATE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate_capability" data-raw-source="[&lt;strong&gt;KSRATE_CAPABILITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate_capability)"><strong>KSRATE_CAPABILITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Pin で速度の変更が許可されている場合、または位相的関連の pin 間のインターフェイスが異なる場合は、KSK プロパティ\_STREAM\_RATECAPABILITY を実装する必要があり、その結果、異なるタイムスタンプ形式が使用されます。 また、プロパティを使用して、"劣化要求のスキップ" など、一般的なタイムスタンプ形式を変換することもできます。

プロパティは、再サンプリングまたはタイムスタンプの変更によってデータの速度を変更するピンによってサポートされます。 すべてのレートの変更では、レートを要求し、特定の pin がどの程度修正して公称1.0 率を取得できるかを判断します。 たとえば、ビデオ再生率2.0 を要求する pin は、ビデオクリップの公称レートの2倍にレンダリングするように指示します。速度要求0.5 は、30倍速レンダリングを意味します。

レート要求には、プレゼンテーションの開始時刻とそのレート要求の期間の両方が含まれています。 これにより、データストリームの特定の部分に適用される制約を考慮することができます。 プレゼンテーション時間、分子/分母のペア、および期間の単位は、構造体で指定されたインターフェイスの観点から表現されます。 標準インターフェイスが使用されていない場合、初期レートの変更クエリを pin に送信することはできません。

Pin は、同様のトポロジを持つ任意の pin で使用されるインターフェイス識別子を受け入れることができる必要があります。 また、インターフェイス識別子と時間単位をそれぞれの対応する値に変換する必要があります。 この方法では、クライアントは既知のインターフェイスポイントからグラフを走査し、各ステップの接続ポイントによって単位を変換できます。

レートの変更が行われない場合でもインターフェイスの変更を行う場合は、このプロパティをサポートすることが重要です。そのため、クエリを実行するときにインターフェイスと時間単位を調整できます。 結果として返されるレートは変更されませんが、インターフェイス、プレゼンテーション開始、および期間は変わります。

レート機能の要求は、一時停止または実行状態でのみ実行でき、他の状態に変更した後は無効になります。 レートが最初の1.0 であるクエリは、通常、タイムスタンプ形式を変換する要求であるため、常に成功する必要があります。

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


[**KSRATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)

[**KSRATE\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate_capability)

 

 






