---
title: KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード
description: KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード プロパティは、デバイスで利用可能なテレビ オーディオ モードを取得します。 このプロパティを実装する必要があります。
ms.assetid: 9c98771a-7a41-469d-a441-da5c1ac5a697
keywords:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2837e60b2a762cb974725c35f0c68b56c0ff055
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355961"
---
# <a name="kspropertytvaudiocurrentlyavailablemodes"></a>KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード


KSPROPERTY\_TVAUDIO\_現在\_利用可能な\_モード プロパティは、デバイスで利用可能なテレビ オーディオ モードを取得します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tvaudio_currently_available_modes_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tvaudio_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、現在使用できるテレビ オーディオ モード、ステレオまたはモノラル オーディオおよび複数の言語設定などを指定する ULONG。

<a name="remarks"></a>注釈
-------

**モード**、KSPROPERTY のメンバー\_TVAUDIO\_の構造は、オーディオ モードを指定します。 KS のビットごとの or 演算が含まれている\_TVAUDIO\_モード\_\*情報が要求された時点で、デバイスでサポートされるモードを示すフラグ。

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

[**KSPROPERTY\_TVAUDIO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)

 

 






