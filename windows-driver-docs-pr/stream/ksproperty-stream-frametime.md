---
title: KSPROPERTY\_ストリーム\_FRAMETIME
description: KSPROPERTY\_ストリーム\_FRAMETIME プロパティにより、クライアントは、特定のメディア ストリームに基づいて次のフレームの継続時間を特定して、手順フレームにその情報を使用するシーケンス。
ms.assetid: 0cc218eb-1f21-4b45-ac48-b3e308bddfaf
keywords:
- KSPROPERTY_STREAM_FRAMETIME ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_FRAMETIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e58877f78599834bd2e874ce1d05df3dea3cdd6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390889"
---
# <a name="kspropertystreamframetime"></a>KSPROPERTY\_ストリーム\_FRAMETIME


KSPROPERTY\_ストリーム\_FRAMETIME プロパティにより、クライアントは、特定のメディア ストリームに基づいて次のフレームの継続時間を特定して、手順フレームにその情報を使用するシーケンス。

## <span id="ddk_ksproperty_stream_frametime_ks"></span><span id="DDK_KSPROPERTY_STREAM_FRAMETIME_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562558" data-raw-source="[&lt;strong&gt;KSFRAMETIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562558)"><strong>KSFRAMETIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_ストリーム\_FRAMETIME は pin が転送には、メディアの種類の詳細を認識しない場合に実装される省略可能なプロパティです。

プロパティは、レンダリング pin ではサポートされてし、データおよびそのフレームに関連付けられているすべてのフラグの次のフレームの継続時間を返すために使用します。 フレームは、一般に、データを分割する最小使用可能な単位です。 ビデオ ストリーム、ビデオのフレームまたはフィールドがあります。 オーディオ ストリーム内の各チャンネル用のサンプルになります。 MIDI の [次へ]、MIDI イベントになります。

期間は、暗証番号 (pin) によって提供されるプレゼンテーション時間単位で測定されます。 これは、インターフェイスとプレゼンテーション時間で使用される分子と分母のペアに依存します。 これは、汎用のファイル リーダーなどの任意のメディアの種類に対応でないストリームには適用されません。

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

[**KSFRAMETIME**](https://msdn.microsoft.com/library/windows/hardware/ff562558)

 

 






