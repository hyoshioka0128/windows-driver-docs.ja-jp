---
title: KSPROPERTY\_ストリーム\_RATECAPABILITY
description: KSPROPERTY\_ストリーム\_RATECAPABILITY プロパティにより、グラフの特定のストリームをフローに関連するすべてのコネクション ポイントを照会するマネージャー (KSPROPERTY 経由で取得した\_PIN\_DATAROUTING) の標準の速度に要求されたレートを調整することで機能します。
ms.assetid: 73e3bf4e-2815-4890-ba12-77fbe7a7c589
keywords:
- KSPROPERTY_STREAM_RATECAPABILITY ストリーミング メディア デバイス
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
ms.openlocfilehash: 77dbfcd29ae981c4efafcb89c466b7139241c32b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548959"
---
# <a name="kspropertystreamratecapability"></a>KSPROPERTY\_ストリーム\_RATECAPABILITY


KSPROPERTY\_ストリーム\_RATECAPABILITY プロパティにより、グラフの特定のストリームをフローに関連するすべてのコネクション ポイントを照会するマネージャー (KSPROPERTY 経由で取得した\_PIN\_DATAROUTING) の標準の速度に要求されたレートを調整することで機能します。

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
<td><p>X</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566752" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566752)"><strong>KSRATE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566754" data-raw-source="[&lt;strong&gt;KSRATE_CAPABILITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566754)"><strong>KSRATE_CAPABILITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_ストリーム\_RATECAPABILITY を実装する場合は、暗証番号 (pin) は、レートの変化、または位相的に関連するピンの間のインターフェイスが異なると、さまざまなタイムスタンプ形式が使用されます。 プロパティは、一般に、タイムスタンプ形式など、パフォーマンス低下の要求をスキップする時間の変換にも使用できます。

Pin を再サンプリングを使用してデータの割合を変更して、プロパティがサポートされているまたはタイムスタンプを変更します。 レートのすべての変更では、要求レートと公称 1.0 レートを取得するには、そのレートを修正できる量を特定の pin を決定する必要があります。 2.0 のビデオの再生速度を要求する pin ビデオ クリップの少額の料金 2 回で表示するために、要求が高ければ、たとえば、0.5 の価格の要求は、半分の速度のレンダリングからわかるようにします。

価格の要求には、プレゼンテーションの開始時刻とその価格の要求の実行時間の両方が含まれています。 これにより、アカウントにあるデータ ストリームの特定の部分に適用される制約。 プレゼンテーション時間では、分子と分母のペア、および期間の単位は、構造体で指定されたインターフェイスの観点から表現されます。 標準的なインターフェイスを使用しない場合は、pin の初期速度の変更クエリを送信できません。

Pin は、ようなトポロジを使用した pin で使用されるインターフェイスの識別子をそのまま使用できる必要があります。 対応する値にインターフェイス識別子と時間の単位に変換する必要があります。 この方法でクライアントは既知のインターフェイスを 1 つのポイントから、グラフを走査し、ユニットがある方法は、の各ステップでの接続ポイントによって変換されます。

レートの変化にできない、その場合でも、インターフェイスの変更が加えられた場合は、このプロパティをサポートすることが重要、インターフェイスであり、クエリが行われたときに、時間単位を調整できます。 結果は返されるレートは変化しませんが、インターフェイス、PresentationStart、および期間の変更は。

機能要求のレートを一時停止または実行の状態で実行のみと他の状態を変更した後で無効になります。 タイムスタンプの形式の時間を変換するだけで要求を通常はクエリの速度が 1.0 で、最初に常に成功します。

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


[**KSRATE**](https://msdn.microsoft.com/library/windows/hardware/ff566752)

[**KSRATE\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566754)

 

 






