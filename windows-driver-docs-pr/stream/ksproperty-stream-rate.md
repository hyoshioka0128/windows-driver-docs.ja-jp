---
title: KSK プロパティ\_STREAM\_RATE
description: KSK プロパティ\_STREAM\_RATE プロパティは、KSK プロパティ\_STREAM\_RATECAPABILITY と共に動作し、pin の機能を照会した後にセグメントの比率を設定するために使用されます。
ms.assetid: 125dcd39-fb67-4d9f-81af-b7f4c0e566cc
keywords:
- KSPROPERTY_STREAM_RATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_RATE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e384b69f27f35b1275ee52efe81228944acc009
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837942"
---
# <a name="ksproperty_stream_rate"></a>KSK プロパティ\_STREAM\_RATE


KSK プロパティ\_STREAM\_RATE プロパティは、 [**Ksk プロパティ\_stream\_RATECAPABILITY**](ksproperty-stream-ratecapability.md)と共に動作し、pin の機能を照会した後にセグメントの比率を設定するために使用されます。

## <span id="ddk_ksproperty_stream_rate_ks"></span><span id="DDK_KSPROPERTY_STREAM_RATE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)"><strong>KSRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Pin で速度の変更が許可される場合、または位相的関連のピン間のインターフェイスが異なる場合に、KSK プロパティ\_ストリームの\_率を実装する必要があり、その結果、異なるタイムスタンプ形式が使用されます。

このプロパティは、再サンプリングまたはタイムスタンプの変更によってデータの比率を変更できるピンによってサポートされます。これにより、要求されたレートが1.0 の公称値に近づくことができます。

プロパティを読み取ると、現在のレートとセグメントが返されます。 新しいセグメントのレートを設定すると、現在のレート設定が置き換えられます。 この方法では、速度の設定1.0 を要求することで、高速転送要求を停止できます。これは常に受け入れられる必要があります。 指定したレートを取得できない場合、pin は最適な設定を試みる代わりに要求を拒否できます。

レートの設定とクエリはどちらも、プレゼンテーションの開始、期間、およびレートを指定する[**Ksk レート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)構造を使用します。 比率の変更は、一時停止または実行状態でのみ実行でき、他の状態に変更すると停止されます。 比率の変化は、ピンがに対して調整され、現在の設定が同じ形式で返されることを示す、公称1.0 の割合で指定します。

このプロパティは、前のプロパティで指定されたインターフェイスと時間単位を変換する場合にも使用します。レートの変更がサポートされていない場合でも、ピン間のインターフェイスを変更するフィルターに実装する必要があります。 たとえば、KSK インターフェイスをサポートするフィルターは、1つの pin の標準\_位置を\_し、KSK インターフェイスに変換\_、トポロジによって関連付けられた別の pin での標準\_ストリーミングでは、レートの変更がサポートされない場合があります。 フィルターでは、pin とインターフェイスのどちらかで変更要求を受け取り、それ自体のインターフェイスと単位に変更することができます。ただし、このレートは変更されません。

また、pin によってクロックが生成される場合は、速度の変化によって物理的な時間の傾きが変化しないようにする必要があります。これは、レートの一致にクロックを使用しているすべてのクライアントが、基になるハードウェアが公称1.0 率で実行されている場合と同じようになります。 これは、物理的なクロックの傾斜を維持することができない pin は、大きな誤差がなくても、速度調整要求を受け入れることができないことを意味します。

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


[**KSK プロパティ\_STREAM\_RATECAPABILITY**](ksproperty-stream-ratecapability.md)

[**KSRATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)

 

 






