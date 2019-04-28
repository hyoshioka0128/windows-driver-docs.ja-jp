---
title: KSPROPERTY\_TVAUDIO\_キャップ
description: KSPROPERTY\_TVAUDIO\_CAPS プロパティは、テレビのオーディオ デバイスの機能を取得します。 このプロパティを実装する必要があります。
ms.assetid: a5b7348e-0f85-430c-acf0-c35e289ef338
keywords:
- KSPROPERTY_TVAUDIO_CAPS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3076ba9914a91537af3cb7940f0c96502da1e8b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382545"
---
# <a name="kspropertytvaudiocaps"></a>KSPROPERTY\_TVAUDIO\_キャップ


KSPROPERTY\_TVAUDIO\_CAPS プロパティは、テレビのオーディオ デバイスの機能を取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_caps_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565936" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565936)"><strong>KSPROPERTY_TVAUDIO_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、テレビのオーディオ デバイス モノラル オーディオ サポートおよび複数の言語機能と、ステレオなどの機能を指定する ULONG。

<a name="remarks"></a>注釈
-------

**機能**、KSPROPERTY のメンバー\_TVAUDIO\_CAP\_構造がテレビのオーディオ デバイスの機能を指定します。

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

[**KSPROPERTY\_TVAUDIO\_CAP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565936)

 

 






