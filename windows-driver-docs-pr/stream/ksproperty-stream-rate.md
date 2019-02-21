---
title: KSPROPERTY\_ストリーム\_率
description: KSPROPERTY\_ストリーム\_KSPROPERTY と連携するレート プロパティ\_ストリーム\_RATECAPABILITY、暗証番号 (pin) の機能のクエリを実行した後、セグメントの間隔を設定するために使用します。
ms.assetid: 125dcd39-fb67-4d9f-81af-b7f4c0e566cc
keywords:
- KSPROPERTY_STREAM_RATE ストリーミング メディア デバイス
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
ms.openlocfilehash: 364579feb88b0e98ce28825cba30b74a775145be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549506"
---
# <a name="kspropertystreamrate"></a>KSPROPERTY\_ストリーム\_率


KSPROPERTY\_ストリーム\_レート プロパティと連携する[ **KSPROPERTY\_ストリーム\_RATECAPABILITY** ](ksproperty-stream-ratecapability.md)レートを設定するために使用暗証番号 (pin) の機能を照会したセグメント。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566752" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566752)"><strong>KSRATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_ストリーム\_レートの変化により、pin または位相的に関連するピンの間のインターフェイスが異なると、使用されている別の時刻のタイムスタンプの形式で結果、レートを実装する必要があります。

Pin を再サンプリングを使用してデータの間隔を変更できますが、プロパティがサポートされているまたはタイムスタンプ変更要求のレートを 1.0 の標準レートに近いことができるようにします。

プロパティを読み取るには、現在の速度とセグメントが返されます。 新しいセグメントのレートを設定すると、現在速度設定が置き換えられます。 この方法で高速順方向の要求を停止を行う要求レートの設定は 1.0 で、常に受け入れられる必要があります。 指定したレートで取得できない場合、pin は最適設定を実行する代わりに要求を拒否できます。

レートの設定とクエリの両方を使用して、 [ **KSRATE** ](https://msdn.microsoft.com/library/windows/hardware/ff566752)プレゼンテーションの開始、期間、および速度を指定する構造体。 レートの変化はでのみ実行される一時停止または実行の状態および他の状態を変更した後に停止されます。 料金の変更は、パーセンテージまたは公称 1.0 速度を調整する、暗証番号 (pin) があり、同じ形式で返される現在の設定を によって指定されます。

このプロパティは、インターフェイスを翻訳するも使用する必要があり、時間単位が前のプロパティで指定し、レートの変化がサポートされていない場合でも、変更、ピンの間のインターフェイス フィルターに実装する必要があります。 KSINTERFACE をサポートする、フィルターなど、\_標準\_1 つ上の位置に固定して KSINTERFACE に変換されます\_標準\_トポロジによって関連するもう 1 つの pin でのストリーミングにレートの変化を使用することはできません。 フィルターできる必要がありますを pin といずれかのインターフェイスのいずれかの変更要求を実行し、独自のインターフェイスと単位を変更も、料金は変更されません。

生成した場合、pin もクロック、単価が変更する必要がありますので変更できません、物理の時間の傾きレートが一致する、クロックを使用しているクライアントが、基になるハードウェアが公称 1.0 速度で実行されていたかのように傾斜を指定してください。 つまり、物理クロックの傾斜の重要な誤差なく一貫性が保たを保証できない pin がレート調整の要求を受け付けることができません。

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


[**KSPROPERTY\_ストリーム\_RATECAPABILITY**](ksproperty-stream-ratecapability.md)

[**KSRATE**](https://msdn.microsoft.com/library/windows/hardware/ff566752)

 

 






